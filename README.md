# scanwits-site

Static site for **scanwits.com**: documentation (`/docs/`) and terms of use (`/terms/`).
Hosted on GitHub Pages, domain registered at OVH.

## Structure

```
index.html          Home page
docs/index.html     Documentation
terms/index.html    Terms of use (placeholder for now)
404.html            Not-found page
assets/style.css    Shared stylesheet
CNAME               Custom domain for GitHub Pages (scanwits.com)
.nojekyll           Disable Jekyll processing on GitHub Pages
```

## Local preview

```
python -m http.server 8000
```
Then open http://localhost:8000

## Deployment

### 1. GitHub
1. Create a repository (e.g. `scanwits-site`) and push this folder to the `main` branch.
2. Repository **Settings → Pages**: Source = *Deploy from a branch*, branch `main`, folder `/ (root)`.
3. Custom domain: `scanwits.com` (already set by the `CNAME` file).
4. Once DNS is live, tick **Enforce HTTPS**.
5. Recommended: verify the domain in your GitHub account/organization settings → Pages.

### 2. OVH DNS zone (scanwits.com)
OVH control panel → Domain names → scanwits.com → **DNS zone**.

Remove any existing `A` / `AAAA` record on the root (`scanwits.com`) and any existing record on `www`
(often pointing to OVH's default parking page), then add:

| Sub-domain | Type  | Target                     |
|------------|-------|----------------------------|
| *(empty)*  | A     | 185.199.108.153            |
| *(empty)*  | A     | 185.199.109.153            |
| *(empty)*  | A     | 185.199.110.153            |
| *(empty)*  | A     | 185.199.111.153            |
| *(empty)*  | AAAA  | 2606:50c0:8000::153        |
| *(empty)*  | AAAA  | 2606:50c0:8001::153        |
| *(empty)*  | AAAA  | 2606:50c0:8002::153        |
| *(empty)*  | AAAA  | 2606:50c0:8003::153        |
| www        | CNAME | `<github-account>.github.io.` |

Do **not** touch the `MX`, `SPF`/`TXT` or other records used for email.

Sources:
- GitHub Docs — Managing a custom domain for your GitHub Pages site:
  https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site
- OVHcloud — Add a CNAME record:
  https://docs.ovhcloud.com/fr/guides/web-cloud/domains/dns-zone-cname-record-creation
