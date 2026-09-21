# andrewpataleta.com — deploy & demo recipe

Personal freelancer site + demo host. Same idea as the patstudio recipe, but on Andrew's own domain and a separate repo, positioned as personal (not a studio).

## Main site
- Repo: `AndrewwPataleta/andrewpataleta` (public), GitHub Pages from `main` / root.
- `CNAME` file = `andrewpataleta.com`, plus `.nojekyll`.
- Cloudflare (zone `andrewpataleta.com`, id `7833ae6cd7115307649dc1fb54f071b8`):
  - proxied `CNAME @ -> andrewwpataleta.github.io` (CF flattens at apex)
  - proxied `CNAME www -> andrewwpataleta.github.io`
- GitHub Pages custom domain = `andrewpataleta.com`.
- Edit `index.html`, `git push`, done. HTTPS is instant via the Cloudflare edge cert for `*.andrewpataleta.com` / apex.

## Adding a client demo on a subdomain (e.g. `topripz.andrewpataleta.com`)
Mirrors `patstudio-static-deploy-recipe`:
1. Build the static demo folder (index.html + assets + a `CNAME` file containing `<name>.andrewpataleta.com` + `.nojekyll`).
2. New public repo, push to `main`, enable Pages (main/root) via `gh api -X POST repos/AndrewwPataleta/<repo>/pages -f 'source[branch]=main' -f 'source[path]=/'`.
3. Cloudflare proxied `CNAME <name> -> andrewwpataleta.github.io` on this zone (token in `~/.secrets/cf-dns.env`, `CLOUDFLARE_API_TOKEN`).
4. Wait for the Pages build (`built`), then verify `https://<name>.andrewpataleta.com`.

Gotcha: after a proxy toggle, stale DNS cache can give HTTP 000 / TLS altname errors for ~5 min TTL. Not broken, just wait. Avoid the Railway Metal builder for these (jams).

## Why personal, not studio
This domain is Andrew's own freelancer brand hub. Everything he builds himself goes here (portfolio + live demos), presented as one person shipping products, separate from the PatStudio studio identity.
