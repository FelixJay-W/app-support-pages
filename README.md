# App Support Pages

A dependency-free static site for hosting public support, privacy, and terms pages for multiple apps. GitHub Actions deploys everything under `site/` to GitHub Pages.

PhotoGlow is available at these paths after deployment:

- `/photoglow/support/`
- `/photoglow/privacy/`
- `/photoglow/terms/`

Stampora Camera publishes privacy, terms, and support pages under language-first paths:

- `/stampora/en/{privacy,terms,support}/`
- `/stampora/zh-hans/{privacy,terms,support}/`
- `/stampora/zh-hant/{privacy,terms,support}/`

## Before publishing

1. Confirm that the public support contacts can receive mail: `rhb2517@gmail.com` for PhotoGlow and `rhbjlz@outlook.com` for Stampora Camera.
2. Review the PhotoGlow policy against the release build whenever analytics, advertising, cloud processing, accounts, or a new SDK is added.
3. Keep the website text and App Store privacy answers consistent. The current release states that the developer does not collect data through the app.

## Create the GitHub repository

Create a new public repository on GitHub. A descriptive name such as `app-support-pages` is recommended. Do not initialize it with a README because this project already contains one.

Then run:

```bash
cd "/Volumes/rhb/RhbProjects/AppSupportPages"
git add .
git commit -m "Launch app support pages"
git remote add origin https://github.com/GITHUB_USERNAME/app-support-pages.git
git push -u origin main
```

Replace `GITHUB_USERNAME` with the account or organization that owns the repository. If the repository has a different name, use that name in the remote URL and in the public URLs below.

## Enable GitHub Pages

1. Open the repository on GitHub.
2. Go to **Settings > Pages**.
3. Under **Build and deployment**, set **Source** to **GitHub Actions**.
4. Open the **Actions** tab and wait for **Deploy GitHub Pages** to finish successfully.
5. Open the deployment URL shown by the workflow. Test every legal page in a private browser window.

GitHub Pages project-site URLs use this format:

```text
https://GITHUB_USERNAME.github.io/app-support-pages/
https://GITHUB_USERNAME.github.io/app-support-pages/photoglow/support/
https://GITHUB_USERNAME.github.io/app-support-pages/photoglow/privacy/
https://GITHUB_USERNAME.github.io/app-support-pages/photoglow/terms/
```

The repository may remain public because it contains only public website content. GitHub Pages on a private repository depends on the GitHub plan and organization settings.

## App Store Connect values

After deployment, enter the final public URLs in App Store Connect:

| Field | Value |
| --- | --- |
| Support URL | `https://GITHUB_USERNAME.github.io/app-support-pages/photoglow/support/` |
| Privacy Policy URL | `https://GITHUB_USERNAME.github.io/app-support-pages/photoglow/privacy/` |
| Terms link used by the app/paywall | `https://GITHUB_USERNAME.github.io/app-support-pages/photoglow/terms/` |

Use the Support URL in the current app version metadata. Add the Privacy Policy URL in the app's **App Privacy** section. PhotoGlow's paywall must continue to provide visible Privacy Policy, Terms of Use, and Restore Purchases actions.

Before submission, verify that each URL:

- Loads without signing in.
- Uses HTTPS and returns a successful page.
- Works on an iPhone-sized screen.
- Shows PhotoGlow rather than a generic repository page.
- Contains a working support email.
- Does not redirect to a missing custom domain.

## Optional custom domain

GitHub's `github.io` address is accepted by App Store Connect. A custom domain is optional.

To add one later:

1. Configure the domain in **Settings > Pages > Custom domain**.
2. Add the DNS records GitHub specifies.
3. Add a `site/CNAME` file containing only the domain, for example `apps.photoglow.app`.
4. Push the change and enable **Enforce HTTPS** after DNS verification completes.
5. Replace all App Store Connect URLs only after the new HTTPS pages work reliably.

## Add another app

Create another lowercase directory under `site/` using the app's stable URL slug:

```text
site/
  another-app/
    index.html
    support/index.html
    privacy/index.html
    terms/index.html
```

Reuse `site/assets/site.css`, give the app its own icon under `site/assets/`, and add the app to `site/index.html`. Keep each app's privacy policy specific to what that binary actually collects and transmits. A push to `main` deploys all apps together.

## Updating a policy

Update the visible **Last updated** date only when policy content changes. Commit and push the edit, wait for the Pages workflow, then inspect the public page. Preserve previous policy versions in Git history; do not silently change app behavior without updating the policy and App Store privacy answers.
