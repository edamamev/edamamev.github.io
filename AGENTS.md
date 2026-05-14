# AGENTS.md

## Project

Personal Astro site at `edamamev.github.io`. Static site deployed to GitHub Pages.

## Commands

```sh
npm run dev       # dev server
npm run build     # static build -> dist/
npm run preview   # preview built site
```

## CI / Deploy

- GitHub Actions (`.github/workflows/deploy.yml`) builds & deploys to Pages on push to `main`.
- Uses `withastro/action@v6`. Node version defaults to 22; npm is the package manager.

## Architecture

- **Layout**: `src/layouts/Base.astro` — slots: `below-title`, `below-break`
- **Components**: `src/components/` — Header, Footer, Edme (avatar), ListItem, MainTop, Social
- **Content**: `src/pages/articles/*.md` (loaded via `import.meta.glob` in `articles.astro`) and `src/pages/notes/*.md`
- **Styling**: `src/styles/global.css` — dark theme via CSS custom properties
- **Deploy target**: `site: 'https://edamamev.github.io'` in `astro.config.mjs`

## Content frontmatter

Articles (`src/pages/articles/*.md`) use: `title`, `pubDate`, `description`, `author`, `tags`.

## Known issues (agent watchpoints)

- `src/pages/notes.astro` — does **not** load posts (unlike `articles.astro`). Needs `import.meta.glob` for `./notes/*.md`.
- `src/pages/notes/post1.md` — frontmatter uses `pubData` (typo) instead of `pubDate`.
- `src/components/Footer.astro:5` — variable `localRedditSVV` has a typo and is unused.
- `src/components/Social.astro:3` — uses `` `https://www.${platform}.com/${username}` `` with backtick template literal but the syntax is broken (Astro template expressions use `{}`, not backticks directly in attribute position).
- `src/components/Edme.astro` — references `/test.png`; both `/test.png` and `/test1.png` exist in `public/`.
- `src/components/Header.astro` — only Home and Articles links are active; Notes, Bookmarks, Certs, About are commented out.
- Several pages (`about.astro`, `bookmarks.astro`, `certs.astro`, `notes.astro`) contain placeholder text ("Lorem Ipsum" / "Lorum Ipsum").
- `src/pages/meta.astro` — empty file.
- Import of `Edme.astro` in `index.astro` is commented out alongside placeholder content.

## Opencode

`opencode.json` does not exist. No `.cursorrules`, `CLAUDE.md`, or `copilot-instructions.md` present.
