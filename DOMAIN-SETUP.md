# Setting Up covalent-ai.dev with GitHub Pages

## Overview

Connect your Namecheap domain `covalent-ai.dev` to your GitHub Pages site at `covalent-dev.github.io`.

## Step 1: Namecheap DNS Configuration

1. Log into Namecheap → Domain List → `covalent-ai.dev` → Manage
2. Go to **Advanced DNS** tab
3. Delete any existing A records or CNAME records for `@` or `www`
4. Add these records:

### For apex domain (covalent-ai.dev):

| Type | Host | Value | TTL |
|------|------|-------|-----|
| A | @ | 185.199.108.153 | Automatic |
| A | @ | 185.199.109.153 | Automatic |
| A | @ | 185.199.110.153 | Automatic |
| A | @ | 185.199.111.153 | Automatic |

### For www subdomain:

| Type | Host | Value | TTL |
|------|------|-------|-----|
| CNAME | www | covalent-dev.github.io. | Automatic |

**Note:** The CNAME value should end with a period (`.`) in some DNS providers.

## Step 2: GitHub Repository Configuration

1. Go to https://github.com/covalent-dev/covalent-dev.github.io
2. Settings → Pages (left sidebar)
3. Under "Custom domain", enter: `covalent-ai.dev`
4. Click Save
5. Wait for DNS check to pass (can take a few minutes)
6. Check "Enforce HTTPS" once available

## Step 3: Add CNAME File to Repo

Create a file called `CNAME` (no extension) in the repo root:

```
covalent-ai.dev
```

This tells GitHub Pages which domain to serve.

```bash
cd ~/covalent-dev/covalent-dev.github.io
echo "covalent-ai.dev" > CNAME
git add CNAME
git commit -m "add custom domain"
git push origin main
```

## Step 4: Verify

1. Wait 5-30 minutes for DNS propagation
2. Check DNS: `dig covalent-ai.dev +short` (should show GitHub IPs)
3. Visit https://covalent-ai.dev
4. Visit https://www.covalent-ai.dev (should redirect to apex)

## Troubleshooting

**"DNS check failed"** — Wait longer, DNS can take up to 48 hours (usually 5-30 min)

**Certificate error** — HTTPS cert takes a few minutes after DNS propagates. Wait and retry.

**404 on custom domain** — Make sure CNAME file exists and matches exactly.

**Still pointing to old site** — Clear browser cache or try incognito.

## Verification Commands

```bash
# Check A records
dig covalent-ai.dev A +short

# Check CNAME for www
dig www.covalent-ai.dev CNAME +short

# Check if site is up
curl -I https://covalent-ai.dev
```

## Timeline

- DNS changes: 5-30 minutes (up to 48h worst case)
- HTTPS certificate: 5-15 minutes after DNS propagates
- Total: Usually under 1 hour

---

Once set up, both `covalent-ai.dev` and `www.covalent-ai.dev` will serve your GitHub Pages site with HTTPS.
