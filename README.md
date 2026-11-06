# project-html

A static HTML site deployed to [Vercel](https://vercel.com). Every `git push` to
`main` triggers an automatic production deployment.

## How it works

- This repo holds plain `.html` files at the project root.
- Vercel is connected to this GitHub repository via its Git integration.
- Pushing to `main` → Vercel builds and deploys automatically.
- Each HTML file is served as its own page at the site root.

```
repo root/
├── index.html      # landing page  →  /
├── page.html       # →  /page
└── vercel.json     # Vercel config (static, cleanUrls)
```

Because `cleanUrls` is enabled in `vercel.json`, `page.html` is reachable at
`/page` (the `.html` URL redirects there). To disable that, remove `"cleanUrls": true`.

## One-time setup

1. **Add your SSH key to GitHub** (only needed once per machine):
   ```bash
   cat ~/.ssh/id_ed25519.pub
   ```
   Paste the output at https://github.com/settings/keys, then verify:
   ```bash
   ssh -T git@github.com
   ```

2. **Create the GitHub repo** at https://github.com/new
   (name it `project-html`, do **not** initialize with a README), then connect and push:
   ```bash
   git remote add origin git@github.com:<your-username>/project-html.git
   git push -u origin main
   ```

3. **Import into Vercel** at https://vercel.com/new
   → *Import Git Repository* → select `project-html` → Framework Preset: **Other** → **Deploy**.

After this, deployments are automatic — no Vercel CLI required.

## Deploying a new page

```bash
# 1. add your file(s) to the project root
# 2. commit and push
git add .
git commit -m "add new page"
git push
```

Vercel deploys within a minute or so. The new page goes live at:

```
https://<project-name>.vercel.app/<filename>
```

You can also track the build and get the live URL from the Vercel dashboard
under the project's **Deployments** tab.

## Notes

- `.commandcode/` and `.vercel/` are gitignored (local tool state — not deployed).
- `index.html` is a placeholder landing page; replace it with your own.
- No build step, no dependencies — Vercel serves the files as-is.
- Preview deployments: pushing to any branch other than `main` produces a preview
  URL instead of updating production.
