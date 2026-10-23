# Hamza Kheddar — Academic Homepage

Responsive static academic website for GitHub Pages, with GitHub-backed announcement manager, Google Analytics 4 integration instructions, and SEO files.

## Publish on GitHub Pages

1. Create a **public** GitHub repository named `YOUR_USERNAME.github.io` (recommended), or any repository name.
2. Upload all the files and folders in this package to the repository root (not the ZIP itself).
3. In **Settings → Pages**, select **Deploy from a branch**, `main`, folder `/ (root)`; save. Your site will appear at `https://YOUR_USERNAME.github.io/` (or `/REPOSITORY/` for project repos).
4. For project repos, relative asset paths work, but the sitemap and canonical URL must include `/REPOSITORY/`.
5. Replace `assets/profile-placeholder.svg` by adding `assets/profile.jpg` (a real JPG portrait). The page will automatically use it.
6. Replace the placeholder X/Twitter text in `index.html` with your actual link when available.
7. Replace the placeholder GitHub owner/repository in `assets/site.js` (the GitHub API news fetch URL) so fresh announcements can appear even before CDN refresh. The fallback local JSON works without this.
8. Edit `sitemap.xml` to the real public site URL; optionally add a `Sitemap:` directive to `robots.txt`. Register the property in Google Search Console, verify ownership and submit `sitemap.xml`.
9. Optionally buy a custom domain and configure it in GitHub Pages settings with DNS records as directed by GitHub. Then update the sitemap and Search Console property.

## Announcements: browser-based admin

Visit `https://YOUR_USERNAME.github.io/admin/` (or `/REPOSITORY/admin/`). Enter the owner, repository, `main` branch, and a **fine-grained GitHub personal access token** scoped to this repository with **Contents: Read and write** only. Click **Load announcements**, edit/add/delete, and **Publish changes to GitHub**.

**Security:** The token is used only in memory and sent directly to `api.github.com` using HTTPS. It is never saved to localStorage, a cookie, or your repository. This is not a private login page; anyone can visit `/admin/`, but only authorized GitHub token holders can commit. Do not use broad classic tokens or paste a token into the public website source. Revoke the token if exposed. For stronger administration security, use GitHub's own repository editor rather than the browser admin. GitHub API CORS support is required by this admin workflow.

To update announcements without a token, edit `content/announcements.json` directly in GitHub's web interface and commit.

## Google Analytics 4: country tracking

1. Create a GA4 property and a **Web** data stream at https://analytics.google.com/.
2. Copy the measurement ID, e.g. `G-XXXXXXXXXX`.
3. Add the following **before `</head>`** in `index.html`, replacing the ID in both locations:

```html
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX');
</script>
```

4. In GA4, check **Reports → User attributes → Demographic details → Country** (menu labels may change). This shows country-level visitors once traffic is collected. GA4 does not retroactively collect earlier traffic. Some visitors may be grouped under unknown locations; VPNs and consent choices affect accuracy.
5. Check your region's privacy and consent requirements. If consent is required, deploy an appropriate consent management solution and prevent analytics tracking until consent is obtained. Add a privacy notice. Do not publish individual visitors' IP addresses or detailed personal data.

**Note:** GA4 credentials and actual country statistics cannot be generated or displayed before the user creates a GA4 property and deploys the site. This package provides the integration instructions, not a working measurement ID.

## Customize

- Main page: `index.html`
- Colors and responsive layout: `assets/style.css`
- News: `content/announcements.json` and `admin/`
- Profile photo: `assets/profile.jpg`
- SEO: `<title>`, description, Person JSON-LD, `sitemap.xml`, `robots.txt`
- CV: Add a PDF as `assets/Hamza_Kheddar_CV.pdf` and link it from the page (not bundled; the CV is personal source material).

The sample news entries are editable and publication titles/statuses should be verified before public launch. Search engine indexing is not guaranteed.
