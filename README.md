# Body

个人健康记录：体重、腰围、跑步、喝酒，医院检查项目和体检报告（可用 Claude 自动整理异常指标）。

纯静态网页，不需要服务器，部署到 GitHub Pages 即可在手机和电脑上使用。

## 文件说明

| 文件 | 作用 |
| --- | --- |
| `index.html` | 整个应用（页面、样式、逻辑都在这一个文件里） |
| `manifest.webmanifest` | 让网页可以“添加到主屏幕”，像 App 一样全屏打开 |
| `sw.js` | 离线缓存，没网也能打开和记录 |
| `icons/` | 应用图标 |
| `.nojekyll` | 告诉 GitHub Pages 原样发布文件 |

## 部署步骤

1. 登录 GitHub，点右上角 **+ → New repository**，仓库名填 `body`（或任意名字），选 **Public**，点 **Create repository**。
   - 免费账号的 GitHub Pages 需要公开仓库。仓库里只有程序文件，**你的健康数据不在仓库里**，不会被公开。
2. 在新仓库页面点 **uploading an existing file**，把本文件夹里的所有内容（`index.html`、`manifest.webmanifest`、`sw.js`、`README.md`、`.nojekyll`、`icons` 文件夹）拖进去，点 **Commit changes**。
   - `.nojekyll` 是隐藏文件，网页上传时如果看不到可以跳过，不影响使用。
3. 进入仓库的 **Settings → Pages**，在 **Build and deployment** 里：
   - Source 选 **Deploy from a branch**
   - Branch 选 **main**，文件夹选 **/ (root)**，点 **Save**
4. 等 1～2 分钟，刷新这个页面，顶部会出现网址，形如 `https://你的用户名.github.io/body/`。打开就能用。

以后要更新，只需在仓库里替换 `index.html` 再提交，几分钟后生效。

## 导入已有数据

1. 打开部署好的网址，点底部 **我的**。
2. 在 **数据备份 → 从备份恢复** 里选择 `Body备份-2026-10-19.json`，点 **恢复**。

> ⚠️ 不要把备份文件上传到 GitHub 仓库里，那样会公开你的数据。

## 添加到手机主屏幕

- **iPhone**：用 Safari 打开网址 → 分享按钮 → **添加到主屏幕**
- **安卓**：用 Chrome 打开网址 → 右上角菜单 → **添加到主屏幕 / 安装应用**

## 数据保存在哪里

- 所有记录和附件保存在**当前浏览器**里（IndexedDB），不会上传到任何服务器。
- 不同设备、不同浏览器之间**不会自动同步**。换设备时：旧设备 **导出完整备份** → 新设备 **从备份恢复**。完整备份包含附件。
- 清除浏览器网站数据会删除记录，建议定期导出备份。

## 体检报告自动识别

自动识别异常指标需要你自己的 Claude API Key：

1. 在 [console.anthropic.com](https://console.anthropic.com) 创建 API Key。
2. 在 Body 的 **我的 → 资料与目标** 里填入 Key，点 **保存设置**。

Key 只保存在你这台设备的浏览器里，导出的备份文件不会包含它。识别时，报告内容会直接从你的浏览器发送到 Anthropic 接口，按 API 用量计费。不填 Key 也可以手动添加异常指标。
