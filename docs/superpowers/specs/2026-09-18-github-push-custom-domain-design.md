# Design: Push to GitHub + Custom Domain (jagoweb.biz.id)

## 1. Background & Objectives
- **Project**: Jago Web landing page (`d:\jago-web`) containing static web files (`index.html`, `robots.txt`, `sitemap.xml`, `CNAME`).
- **Target Repository**: GitHub account `usupsupriadi`, new repository `jago-web` (Public).
- **Hosting Platform**: GitHub Pages (free, automated static hosting directly from `main` branch).
- **Custom Domain**: `jagoweb.biz.id` (Apex domain) with CNAME for `www.jagoweb.biz.id`.
- **DNS Provider**: Domainesia / Rumahweb / IDwebhost (cPanel DNS Zone Editor).

## 2. GitHub Repository & Deployment Architecture
- **Repository Name**: `jago-web`
- **Visibility**: Public (required for free GitHub Pages custom domain hosting without GitHub Pro/Team plan).
- **Remote Configuration**: Set `origin` to `https://github.com/usupsupriadi/jago-web.git`.
- **Push Branch**: `main`
- **Pages Source**: Branch `main`, path `/` (root).
- **Custom Domain Setting**: Set to `jagoweb.biz.id` via GitHub repository settings or CLI API.
- **HTTPS**: Enforce HTTPS once DNS records are verified and SSL certificate is issued by Let's Encrypt / GitHub.

## 3. DNS Configuration Details
Registrar DNS Zone Editor must have the following records:
1. **Apex / Root Domain (`jagoweb.biz.id`)**:
   - `A` record -> `185.199.108.153`
   - `A` record -> `185.199.109.153`
   - `A` record -> `185.199.110.153`
   - `A` record -> `185.199.111.153`
2. **Subdomain (`www.jagoweb.biz.id`)**:
   - `CNAME` record -> `usupsupriadi.github.io.`
3. **Conflict Cleanup**:
   - Remove any previous default parked / placeholder `A` records on `@` or `jagoweb.biz.id`.

## 4. Verification Plan
- Verify repo created on GitHub: `gh repo view usupsupriadi/jago-web`
- Verify git remote and push success: `git status`, `git branch -vv`
- Verify GitHub Pages enabled: `gh api repos/usupsupriadi/jago-web/pages`
- Check DNS propagation using PowerShell `Resolve-DnsName jagoweb.biz.id`
