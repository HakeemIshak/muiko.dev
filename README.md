# muiko.dev

the promo page for muiko. plain html, no build.

```sh
python3 -m http.server 8000   # http://localhost:8000
```

## files
- `index.html` — the whole page: css, the facade svg, ~40 lines of js, all inline
- `fonts/` — fraunces + doto, latin only, from google fonts (OFL)
- `og.html` → `og.png` — the social card. re-render after editing og.html:
  ```sh
  python3 -m http.server 8000 &
  "/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new --hide-scrollbars \
    --force-device-scale-factor=1 --window-size=1200,630 --virtual-time-budget=2000 \
    --user-data-dir=/tmp/og-chrome --screenshot="$PWD/og.png" http://localhost:8000/og.html
  ```
- `_headers`, `robots.txt`, `sitemap.xml`, `404.html` — cloudflare pages plumbing

## to change
- sponsor button → the `href` on `#sponsor-link` in `index.html`
- footer status link → add `uptime.muiko.dev` once it's green (redeploy the shortener so `/api/health` exists)
- rooms → the `#rooms` list; facade windows deep-link to `#room-<name>`

## deploy
push to `master`. cloudflare pages serves the repo root. keep pages web analytics off (the csp blocks its beacon, and the footer says no tracking).
