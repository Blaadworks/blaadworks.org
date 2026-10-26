# blaadworks.org

Website of the Blaadworks organization, served at https://blaadworks.org (`site` in `astro.config.mjs`). Static site on Astro 7 (`output: "static"`), no integrations, no UI frameworks, plain scoped `<style>` in `.astro` files. Licensed under GPL-3.0.

The whole site is a single page: a centered `Blaadworks: <phrase>` heading, the phrases in gray. The phrases sit on the faces of a four-sided 3D box that rolls top-to-bottom to the next face (1 s still, 0.5 s turn). The box always has 4 faces regardless of the phrase count: the script writes the next phrases onto faces while they are turned away, and hidden `.sizer` copies of all phrases keep the box as wide as the longest one; the user can drag it vertically to spin it, on release it keeps spinning with inertia and decelerates onto a face, then auto-rotation resumes. Text selection and the context menu are disabled. Background is pure black or pure white following the system color scheme. `README.md` is still the Astro starter text.

## Layout

- `src/pages/index.astro` — the page: heading, phrase list, the prism and its rotation/drag script
- `src/layouts/Layout.astro` — the HTML shell (`<head>`, title, favicon), global light/dark colors and font
- `astro.config.mjs` — the site font: Inter (variable, 100–900) via Astro's built-in Fonts API from the Google provider; it is downloaded at build time and self-hosted, exposed as `--font-inter`
- `public/` — files served as is (`favicon.svg`)

## Commands

- `npm run dev` — dev server at `localhost:4321`; to run it from an agent use `npx astro dev --background` and stop it with `npx astro dev stop` (see `AGENTS.md`)
- `npm run build` — build to `dist/`; use it to verify changes
- `npm run preview` — serve the built `dist/`

`astro check` is not available: `@astrojs/check` and `typescript` are not installed. Don't add them unless asked.

Node `>=22.12.0`. Dependencies are kept at the latest Astro; when bumping, update the range in `package.json` to the installed version too.

## Deploy

Self-hosted on Blaadick's home server. `.github/workflows/deploy.yaml` runs on every push to `master` (or manually): builds the site and rsyncs the contents of `dist/` over SSH to `/srv/http/blaadworks.org/`. It needs the repository secrets `SSH_KEY`, `SSH_HOST` and optionally `SSH_PORT`. The workflow mirrors the one in `blaadick.blaadworks.org`; keep them in sync. Don't touch the server or deploy anything yourself.

## Code style

No formatter config; the project is edited in WebStorm. Match the existing files:

- 4-space indentation everywhere (including JSON)
- single quotes in JS/TS, no spaces inside import braces: `import {defineConfig} from 'astro/config';`
- self-closing tags without a space: `<slot/>`, `<meta charset="utf-8"/>`

## Git

Short subject-only commits in past/imperative form, e.g. `Update Astro`, `Update modules`.
