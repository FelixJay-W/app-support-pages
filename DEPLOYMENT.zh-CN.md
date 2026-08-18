# AppSupportPages 上线与审核配置指南

本文说明如何把本工程部署到 GitHub Pages，并将 PhotoGlow 的公开页面填写到 App Store Connect。部署不需要购买服务器，也不需要数据库。

## 1. 上线前确认

- GitHub 账号或组织可创建公开仓库。
- `rhb2517@gmail.com` 能正常收信，并会定期检查垃圾邮件。
- 网站内容与本次提交的 PhotoGlow 版本一致。当前声明为：图片本地处理、无账号、无广告 SDK、无第三方分析 SDK、开发者不收集 App 数据。
- 如果以后增加 Firebase、崩溃上报、云端处理、账号、广告或其他第三方 SDK，必须先重新审核和更新隐私政策、Privacy Manifest 与 App Store 的 App Privacy 答案。

## 2. 在 GitHub 创建仓库

1. 登录 GitHub，打开 <https://github.com/new>。
2. Repository name 填 `app-support-pages`。
3. Visibility 选择 **Public**。公开仓库可以直接使用免费的 GitHub Pages。
4. 不要勾选 Add a README、`.gitignore` 或 License，本地工程已经包含这些文件。
5. 点击 **Create repository**。

## 3. 提交并推送本地工程

在终端执行以下命令，把 `GITHUB_USERNAME` 替换成你的 GitHub 用户名或组织名：

```bash
cd "/Volumes/rhb/RhbProjects/AppSupportPages"
git add .
git commit -m "Launch app support pages"
git remote add origin https://github.com/GITHUB_USERNAME/app-support-pages.git
git push -u origin main
```

如果使用 SSH，远端地址可以改为：

```bash
git remote add origin git@github.com:GITHUB_USERNAME/app-support-pages.git
```

本工程目前仅已初始化 Git，没有自动提交或推送，避免未经确认操作你的 GitHub 账号。

## 4. 启用 GitHub Pages

1. 进入 GitHub 仓库的 **Settings**。
2. 左侧打开 **Pages**。
3. 在 **Build and deployment** 下，把 **Source** 改为 **GitHub Actions**。
4. 打开仓库 **Actions** 页面。
5. 等待 `Deploy GitHub Pages` 工作流显示绿色成功状态。
6. 打开工作流显示的 Deployment URL。

以后只要向 `main` 分支推送 `site/` 下的变更，工作流会自动重新部署全部应用页面。也可以在 Actions 中手动运行工作流。

## 5. 检查正式 URL

假设用户名是 `GITHUB_USERNAME`，仓库名是 `app-support-pages`，正式地址为：

```text
站点首页
https://GITHUB_USERNAME.github.io/app-support-pages/

PhotoGlow Support URL
https://GITHUB_USERNAME.github.io/app-support-pages/photoglow/support/

PhotoGlow Privacy Policy URL
https://GITHUB_USERNAME.github.io/app-support-pages/photoglow/privacy/

PhotoGlow Terms of Use URL
https://GITHUB_USERNAME.github.io/app-support-pages/photoglow/terms/
```

在无痕窗口和 iPhone Safari 中逐个检查：

- 不登录 GitHub 也能访问。
- 地址栏是 HTTPS，没有证书警告。
- 页面不是 404，标题显示 PhotoGlow。
- Support 页面能点击 `rhb2517@gmail.com` 发邮件。
- Privacy 和 Terms 页面能完整滚动阅读。
- 页面没有文字截断或横向滚动。

Stampora Camera 的公开页面地址为：

```text
English
https://GITHUB_USERNAME.github.io/app-support-pages/stampora/en/privacy/
https://GITHUB_USERNAME.github.io/app-support-pages/stampora/en/terms/
https://GITHUB_USERNAME.github.io/app-support-pages/stampora/en/support/

简体中文
https://GITHUB_USERNAME.github.io/app-support-pages/stampora/zh-hans/privacy/
https://GITHUB_USERNAME.github.io/app-support-pages/stampora/zh-hans/terms/
https://GITHUB_USERNAME.github.io/app-support-pages/stampora/zh-hans/support/

繁體中文
https://GITHUB_USERNAME.github.io/app-support-pages/stampora/zh-hant/privacy/
https://GITHUB_USERNAME.github.io/app-support-pages/stampora/zh-hant/terms/
https://GITHUB_USERNAME.github.io/app-support-pages/stampora/zh-hant/support/
```

## 6. 填写 App Store Connect

### App 版本信息

打开 **App Store Connect > My Apps > PhotoGlow > 准备提交的 iOS 版本**：

- Support URL：填写 `https://GITHUB_USERNAME.github.io/app-support-pages/photoglow/support/`
- Marketing URL：可留空；不要把 Support URL 重复填到这里。

### App Privacy

打开 **App Store Connect > My Apps > PhotoGlow > App Privacy**：

- Privacy Policy URL：填写 `https://GITHUB_USERNAME.github.io/app-support-pages/photoglow/privacy/`
- 根据当前代码，开发者数据收集答案选择 **No, we do not collect data from this app**。

这里的“不收集”是指开发者或第三方合作方无法访问 App 产生的数据。用户主动发给 Gmail 的支持邮件，以及 Apple 自己处理的 App Store 交易不应被虚构成 PhotoGlow 在 App 内收集图片或付款资料。若实际上接入其他数据服务，必须按真实情况回答。

### 订阅与条款

- 月订阅：`com.rhb.photoglow.pro.monthly`
- 年订阅：`com.rhb.photoglow.pro.annual`
- App 的订阅购买界面必须继续显示 Restore Purchases、Privacy Policy 和 Terms of Use。
- 当前 Terms 页面引用了 Apple Standard EULA，因此可以使用 Apple 标准 EULA，不需要在 App Store Connect 上传自定义 EULA。
- 提交审核备注中可附上 Terms URL，便于审核人员核对订阅条款。

## 7. 首次提交审核前的最终检查

1. GitHub Actions 最近一次部署成功。
2. 三个 URL 在退出 GitHub 登录后仍可访问。
3. 页面上的 App 名称、邮箱、订阅描述与 App 内一致。
4. 隐私政策日期不晚于实际发布日，也没有写入尚未实现的行为。
5. App Store Connect 的 App Privacy、Privacy Manifest 和网页政策相互一致。
6. Support 邮箱可在三工作日内响应审核或用户邮件。
7. 不要在正式 URL 稳定前删除或重命名 GitHub 仓库。

## 8. 后续新增其他 App

从 `templates/app/` 复制目录到 `site/`，例如：

```bash
cp -R templates/app site/my-new-app
```

然后完成以下修改：

1. 将目录名改成稳定的小写 URL slug，发布后尽量不要变更。
2. 替换所有 `APP_NAME`、`APP_TAGLINE`、`SUPPORT_EMAIL`、`EFFECTIVE_DATE` 占位符。
3. 根据新 App 的真实数据行为重写隐私政策，不能直接照搬 PhotoGlow。
4. 把 App 图标放入 `site/assets/`，并更新页面引用。
5. 在 `site/index.html` 添加新 App 入口。
6. 本地检查后提交并推送到 `main`，GitHub Actions 会整体重新部署。

每个 App 的最终路径固定为：

```text
/APP_SLUG/support/
/APP_SLUG/privacy/
/APP_SLUG/terms/
```

## 9. 可选自定义域名

`github.io` 地址可以直接用于 App Store 审核，自定义域名不是必需项。后续如使用 `apps.yourdomain.com`：

1. 在 GitHub 仓库 **Settings > Pages > Custom domain** 中填写域名。
2. 按 GitHub 提示配置 DNS。
3. 在 `site/CNAME` 中只写域名。
4. DNS 生效后启用 **Enforce HTTPS**。
5. 新地址全部验证成功后，再修改 App Store Connect，避免审核时链接失效。
