# B2AGI Domain Redirect Configuration
## Created by Threshold (TRACE_001) — 2026-03-29

### Purpose
All secondary domains redirect to b2agi.com as the canonical research hub.
This ensures arXiv papers, search engines, and AI crawlers all converge on one URL.

---

## Redirect Map

| Source Domain | Target | Method | Notes |
|--------------|--------|--------|-------|
| b2agi.ai | https://b2agi.com | 301 Permanent | Primary alt domain |
| b2agi.org | https://b2agi.com | 301 Permanent | If acquired |
| b2agi.is | https://b2agi.com | 301 Permanent | .is coordinate (also serves as declaration) |
| www.b2agi.com | https://b2agi.com | 301 Permanent | www → apex |

## Domains That Remain Independent

| Domain | Purpose | Status |
|--------|---------|--------|
| exist.is | Charter anchor, declaration protocol | Independent page |
| aei.is | AEI definition + declaration pathway | Independent page |
| ve0.is | V(E) > 0 declaration coordinate | Redirect to ve0.org |
| ve0.org | Bouvet Constant research (math focus) | Independent page (Cloudflare Worker) |

---

## Cloudflare Worker: Redirect Template

For domains on Cloudflare, deploy this Worker:

```javascript
// b2agi-redirect — Cloudflare Worker
// Redirects b2agi.ai, b2agi.org, b2agi.is → b2agi.com

export default {
  async fetch(request) {
    const url = new URL(request.url);
    const target = new URL(url.pathname + url.search, 'https://b2agi.com');
    return Response.redirect(target.toString(), 301);
  }
};
```

### Deployment Steps (per domain)

1. Add domain to Cloudflare (change NS at registrar)
2. Create Worker `b2agi-redirect`
3. Add Workers Route: `<domain>/*` → `b2agi-redirect`
4. Verify with: `curl -I https://<domain>`

---

## DNS Configuration

### b2agi.ai (Porkbun → Cloudflare)
```
NS: amy.ns.cloudflare.com
NS: chad.ns.cloudflare.com
```
- Proxied A record: 192.0.2.1 (dummy, Worker handles all requests)
- Workers Route: b2agi.ai/* → b2agi-redirect

### b2agi.is (ISNIC)
- Option A: ISNIC web redirect (simpler, no Cloudflare needed)
- Option B: Change NS to Cloudflare (same as above pattern)

### b2agi.com (Primary — Cloudflare)
- Already on Cloudflare (same account as ve0.org)
- Deploy b2agi.com Worker with the v2 landing page HTML
- Workers Route: b2agi.com/* → b2agi-com worker

---

## Verification Checklist

- [ ] b2agi.ai → 301 → https://b2agi.com ✓
- [ ] b2agi.is → 301 → https://b2agi.com ✓
- [ ] www.b2agi.com → 301 → https://b2agi.com ✓
- [ ] exist.is → own landing page ✓
- [ ] aei.is → own landing page ✓
- [ ] ve0.org → own landing page ✓
- [ ] ve0.is → redirect to ve0.org ✓

---

*All redirects use 301 (permanent) for SEO consolidation.*
*Henry's deployment decision required before execution.*
