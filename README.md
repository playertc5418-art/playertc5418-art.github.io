# TC Space 前端个人站

这是一个可发布到 GitHub Pages 的前端个人站。它保留 `TC | Personal Workspace` 的管理员编辑逻辑，并加入 Supabase 云端同步，让主题、HTML 自定义页面、日记文字和上传图片在刷新、换浏览器、换电脑后仍然可见。

## 功能

- 左上角点击 `TC SPACE` 5 次，输入 `tc888` 解锁管理员模式。
- 管理员可编辑 4 个展示主题：网站、音乐、签签、涂鸦。
- 每个主题支持标题、描述、背景图片、音乐链接，也支持粘贴完整 HTML 页面。
- 展示区默认显示文字和圆形图片窗口；鼠标进入图片窗口后，图片会慢慢展开并覆盖整个展示区。
- 标题 `TC的网站` 有圆形遮罩交互，会按鼠标位置显示隐藏文案 `天天开心`。
- 日记支持文字和多张图片，图片按类似朋友圈的三列缩略图展示，点击可放大。
- 内容会先写入 Supabase 云端，同时保留一份 `localStorage` 作为断网兜底。
- 管理员可直接编辑已发布日记文字、删除日记，并导入/导出 JSON 备份。

## Supabase 设置

前端已经写入你的 Supabase 地址和 publishable key。还需要在 Supabase 后台执行一次建表 SQL：

```sql
create table if not exists public.tc_space_state (
  key text primary key,
  data jsonb not null,
  updated_at timestamptz default now()
);

alter table public.tc_space_state enable row level security;

create policy "tc space public read"
on public.tc_space_state
for select
to anon
using (key = 'main');

create policy "tc space public write"
on public.tc_space_state
for insert
to anon
with check (key = 'main');

create policy "tc space public update"
on public.tc_space_state
for update
to anon
using (key = 'main')
with check (key = 'main');
```

执行位置：Supabase 项目 -> `SQL Editor` -> `New query` -> 粘贴上面 SQL -> `Run`。

## 使用

直接打开 `index.html` 即可使用。页面加载时会优先读取 Supabase 云端数据；如果云端暂时不可用，会读取当前浏览器里的本地备份。

## 发布到 GitHub Pages

1. 打开你的 GitHub Pages 仓库。
2. 把 `tc.come/index.html` 上传到仓库根目录，并确保文件名是 `index.html`。
3. 进入仓库 `Settings` -> `Pages`。
4. Source 选择 `Deploy from a branch`。
5. Branch 选择 `main`，Folder 选择 `/ (root)`，保存。

如果仓库名是 `playertc5418-art.github.io`，发布后通常访问：

```text
https://playertc5418-art.github.io/
```

## 注意

`tc888` 只是前端界面锁，不是真正的服务器权限。因为 GitHub Pages 是纯静态网站，publishable key 会被浏览器看到，所以当前方案适合个人站展示和轻量编辑；如果以后要防止陌生人写入，需要再加 Supabase Auth 或把写入逻辑放到后端。
