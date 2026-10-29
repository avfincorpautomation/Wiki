# Publishing the wiki to Netlify

The public site is built from `wiki/` only, using Quartz (in the hidden `.quartz/` folder).
`raw/`, `.obsidian/`, `.claude/` and `CLAUDE.md` are listed in `.gitignore` and are never pushed.

## One-time setup

1. On GitHub, create a new **empty** repository (no README), e.g. `aplapollo-wiki`.
   A private repository is fine — Netlify can still build from it, and only the website is public.
2. In this vault folder, run (replace the URL with your repository's):
   ```bash
   git remote add origin https://github.com/<your-username>/aplapollo-wiki.git
   git push -u origin main
   ```
3. On https://app.netlify.com: **Add new site → Import an existing project → GitHub** → pick the repository.
   Leave the build settings as they are — `netlify.toml` already sets them
   (base `.quartz`, command `npx quartz plugin install --from-config && npx quartz build -d ../wiki`, publish `public`). Click **Deploy**.
4. In Netlify: **Site configuration → Change site name** → `aplapollo-wiki`, so the site lives at
   `https://aplapollo-wiki.netlify.app`. If you choose another name or a custom domain, update
   `baseUrl` in `.quartz/quartz.config.yaml` to match.

## Updating the site

After any ingest or lint, push the changes; Netlify rebuilds in about a minute:
```bash
git add -A
git commit -m "Update wiki"
git push
```

## Preview locally

```bash
cd .quartz && npx quartz build --serve -d ../wiki --port 8093
```
Then open http://localhost:8093.
