# GitHub Push and Custom Domain Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Create a public GitHub repository `jago-web`, push the codebase, enable GitHub Pages with custom domain `jagoweb.biz.id`, and provide verified DNS records for Domainesia / Rumahweb / IDwebhost.

**Architecture:** Utilize GitHub CLI (`gh`) to provision `usupsupriadi/jago-web`, link the local git remote `origin`, and push `main`. Enable GitHub Pages targeting the root branch, which reads `CNAME` for `jagoweb.biz.id`. Verify DNS propagation via `Resolve-DnsName`.

**Tech Stack:** Git, GitHub CLI (v2.101.0), GitHub Pages, DNS (A & CNAME Records).

## Global Constraints
- Target user account: `usupsupriadi`
- Repository name: `jago-web`
- Repository visibility: `public`
- Target domain: `jagoweb.biz.id`
- CNAME www domain: `usupsupriadi.github.io.`

---

### Task 1: Create GitHub Repository and Push Code

**Files:**
- Local repo: `d:\jago-web`

- [ ] **Step 1: Create public repository on GitHub and link remote**
```powershell
gh repo create jago-web --public --source=. --remote=origin --push
```

- [ ] **Step 2: Verify remote configuration and push status**
```powershell
git remote -v
git status
gh repo view usupsupriadi/jago-web --json name,url,isPrivate
```

---

### Task 2: Configure GitHub Pages and Custom Domain

**Files:**
- Existing file: `d:\jago-web\CNAME`

- [ ] **Step 1: Check or enable GitHub Pages via GitHub API**
```powershell
gh api -X POST repos/usupsupriadi/jago-web/pages -f "source[branch]=main" -f "source[path]=/"
```
(If already enabled via CNAME push, verify with `gh api repos/usupsupriadi/jago-web/pages`)

- [ ] **Step 2: Verify Custom Domain and HTTPS status in Pages settings**
```powershell
gh api repos/usupsupriadi/jago-web/pages --jq "{cname: .cname, status: .status, html_url: .html_url}"
```

---

### Task 3: DNS Record Checklist & Propagation Verification

**Files:**
- None (External DNS registrar: Domainesia / Rumahweb / IDwebhost)

- [ ] **Step 1: Query current DNS resolution for jagoweb.biz.id**
```powershell
Resolve-DnsName jagoweb.biz.id -Type A
Resolve-DnsName www.jagoweb.biz.id -Type CNAME
```

- [ ] **Step 2: Provide clear DNS Zone Editor guide for user**
Record specifications:
- `A` record `@` -> `185.199.108.153`
- `A` record `@` -> `185.199.109.153`
- `A` record `@` -> `185.199.110.153`
- `A` record `@` -> `185.199.111.153`
- `CNAME` record `www` -> `usupsupriadi.github.io.`
