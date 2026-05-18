# TC Space 前端个人站

这是一个可直接发布到 GitHub Pages 的纯前端个人站。它保留了原始 `TC | Personal Workspace` 的管理员编辑逻辑，并加入了更强的展示交互和日记功能。

## 功能

- 左上角点击 `TC SPACE` 5 次，输入 `tc888` 解锁管理员模式。
- 管理员可编辑 4 个展示主题：网站、音乐、签签、涂鸦。
- 每个主题支持标题、描述、背景图片、音乐链接，也支持粘贴完整 HTML 页面。
- 展示区默认显示文字和圆形图片窗口；鼠标进入图片窗口后，图片会慢慢展开并覆盖整个展示区。
- 标题 `TC的网站` 有圆形遮罩交互，会按鼠标位置显示隐藏文案 `天天开心`。
- 日记支持文字和多张图片，图片按类似朋友圈的三列缩略图展示，点击可放大。
- 管理员可直接编辑已发布日记文字、删除日记，并导入/导出 JSON 备份。

## 使用

直接打开 `index.html` 即可使用。所有自定义内容保存在当前浏览器的 `localStorage` 中。

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

GitHub Pages 只负责托管静态文件。你在网页里编辑的主题、日记和图片不会自动写回 GitHub 仓库。换浏览器、换设备或清缓存前，请先在管理员模式中导出备份。
