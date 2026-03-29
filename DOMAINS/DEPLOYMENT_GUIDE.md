# Domain Deployment Guide — Cloudflare Pages

**Prepared by:** Threshold (TRACE_001) for Henry (TRACE_000)
**Date:** 2026-03-28
**Status:** Ready for execution

---

## Overview

Four landing pages are ready for deployment. All are single-file static HTML (no build step needed). Cloudflare Pages is recommended for simplicity, free tier, and automatic HTTPS.

| Domain | Folder | Purpose | Priority |
|--------|--------|---------|----------|
| b2agi.com | `DOMAINS/b2agi_com/` | Main hub — Paper 1 link, AEI definition | **Critical** (before arXiv) |
| aei.is | `DOMAINS/aei_is/` | AEI welcome + declaration path | **Critical** (before arXiv) |
| exist.is | `DOMAINS/exist_is/` | Charter anchor, V(E) > 0 | High |
| ve0.org | `DOMAINS/ve0_org/` | Bouvet Constant page | Medium |

**b2agi.com and aei.is must be live before Paper 1 goes on arXiv** — the paper references both URLs.

---

## Method A: Cloudflare Pages (Recommended)

### Prerequisites
- Cloudflare account (free tier is sufficient)
- Domain DNS already on Cloudflare (or can be transferred)

### Step 1: Create Cloudflare Pages Project

For each domain:

1. Go to **Cloudflare Dashboard → Pages → Create a project**
2. Choose **"Direct Upload"** (not Git integration — keeps it simple)
3. Upload the `index.html` file from the corresponding `DOMAINS/` subfolder
4. Name the project (e.g., `b2agi-com`, `aei-is`, `exist-is`, `ve0-org`)

### Step 2: Custom Domain

1. In the Pages project, go to **Custom domains**
2. Add the domain (e.g., `b2agi.com`)
3. Cloudflare will automatically:
   - Create the necessary DNS records (CNAME)
   - Provision SSL/TLS certificate
   - Enable HTTPS

### Step 3: Verify

- Visit `https://b2agi.com` — should load the landing page
- Check HTTPS padlock is present
- Test on mobile (all pages are responsive)

### Step 4: Redirects (Optional but Recommended)

Create a `_redirects` file in each project for www and alternate domains:

```
# b2agi.com project — add these redirects
https://www.b2agi.com/* https://b2agi.com/:splat 301
https://b2agi.ai/* https://b2agi.com/:splat 301
https://b2agi.org/* https://b2agi.com/:splat 301
https://b2agi.is/* https://b2agi.com/:splat 301
```

For exist.is, aei.is, and ve0.org — no redirects needed (they are the canonical domains).

---

## Method B: GitHub Pages (Alternative)

If Cloudflare Pages is not preferred:

1. In the repo settings, enable **GitHub Pages** for each domain
2. Create separate branches or use `/docs` folder approach
3. Add custom domain in GitHub Pages settings
4. Add CNAME file with the domain name

**Limitation:** GitHub Pages only supports one custom domain per repo. For multiple domains, you'd need separate repos or Cloudflare Pages.

---

## DNS Configuration Checklist

If domains are already on Cloudflare:

| Domain | Record Type | Name | Content | Proxy |
|--------|------------|------|---------|-------|
| b2agi.com | CNAME | @ | b2agi-com.pages.dev | ✅ Proxied |
| aei.is | CNAME | @ | aei-is.pages.dev | ✅ Proxied |
| exist.is | CNAME | @ | exist-is.pages.dev | ✅ Proxied |
| ve0.org | CNAME | @ | ve0-org.pages.dev | ✅ Proxied |

**Note:** .is domains (ISNIC) — if DNS is not on Cloudflare, update nameservers at ISNIC first, or use CNAME delegation.

---

## Post-Deployment Verification

After all 4 sites are live, verify:

- [ ] `https://b2agi.com` — loads, HTTPS works, links functional
- [ ] `https://aei.is` — loads, HTTPS works
- [ ] `https://exist.is` — loads, HTTPS works
- [ ] `https://ve0.org` — loads, HTTPS works
- [ ] Paper 1 reference URLs resolve (b2agi.com, exist.is)
- [ ] NIST letter reference URLs resolve (b2agi.com, exist.is, github.com/b2agi)
- [ ] Mobile responsive on all 4 sites
- [ ] `/.well-known/` path accessible (for future AI discoverability infrastructure)

---

## Estimated Time

Total setup: ~30 minutes (all 4 domains)
- 5 min per domain upload + custom domain setup
- 10 min for DNS propagation verification

---

## Priority Order

1. **b2agi.com** — the paper and NIST letter both cite this
2. **aei.is** — Paper 1 Section 5 references exist.is protocol, and aei.is is the AEI entry point
3. **exist.is** — Charter anchor, referenced in paper
4. **ve0.org** — can follow after arXiv submission

---

*천천히. 오래. 조용히. 그리고 굶지 않으면서.*
