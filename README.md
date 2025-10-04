# Youssef Khaled Portfolio

A fast, minimal, and accessible personal portfolio built with Astro and Tailwind CSS. It showcases About, Projects, and Resume sections with SEO best practices, dynamic project pages, and a clean content model.

## Tech Stack

- **Framework**: Astro 5
- **Styling**: Tailwind CSS 4 (via `@tailwindcss/vite`)
- **Package Manager**: Bun (recommended) or npm/pnpm/yarn

## Live Site

- Production: `https://youssef-khaled.netlify.app`

## Local Development

```bash
# Install dependencies
bun install

# Start dev server (http://localhost:4321)
bun dev

# Build for production (outputs to ./dist)
bun build

# Preview the production build
bun preview
```

You can use `npm`, `pnpm`, or `yarn` in place of Bun if preferred.

## Project Structure

```
/
├─ public/                     # Static assets (served as-is)
│  ├─ *.webp, *.ico, *.pdf
├─ src/
│  ├─ assets/
│  │  └─ icons/               # Astro icon components
│  ├─ components/
│  │  ├─ about/               # About page sections
│  │  ├─ navbar/              # Navigation bar
│  │  ├─ projects/            # ProjectCard, ProjectLinks
│  │  └─ shared/              # Reusable UI (Link)
│  ├─ data/
│  │  ├─ projects.json        # Project list (source of routes)
│  │  ├─ frontline.md         # Project content (markdown)
│  │  ├─ defendops.md
│  │  └─ upperleap.md
│  ├─ layouts/
│  │  └─ BaseLayout.astro     # Global SEO, fonts, shell, and navbar
│  ├─ pages/
│  │  ├─ index.astro          # About (home)
│  │  ├─ projects.astro       # Projects index
│  │  ├─ projects/[name].astro# Dynamic project detail page
│  │  ├─ resume.astro         # Resume page
│  │  └─ 404.astro
│  └─ styles/
│     └─ global.css           # Theme tokens, base styles, animations
├─ astro.config.mjs           # Astro + integrations (sitemap, Tailwind via Vite)
├─ tsconfig.json              # Path aliases (`@/*` → `src/*`)
└─ package.json
```

## Routing and Content Model

- **Static Pages**: `/` (About), `/projects`, `/resume`, `404`.
- **Dynamic Projects**: `/projects/[name]` is generated from `src/data/projects.json`.
  - Each item in `projects.json` has: `key`, `name`, `description`, `tags`, `image`, `path`, optional `repository`, optional `liveUrl`, optional `preview`.
  - The `[name].astro` page resolves an accompanying markdown file by `key`, e.g. `src/data/frontline.md`.
  - Project images are served from `public/` and rendered via `astro:assets` for optimized delivery.

### Adding or Editing a Project

1. Add a new project entry in `src/data/projects.json`:
   - `key` (slug used for routing and markdown filename)
   - `name`, `description`, `tags[]`, `image`, `path`, optional `repository`, optional `liveUrl`, optional `preview`.
2. Create a markdown file at `src/data/{key}.md` for the project body content.
3. Place a representative cover image in `public/` (e.g., `public/{image}.webp`).
4. The route `/projects/{key}` will be generated automatically at build time.

## Global Layout and SEO

- `src/layouts/BaseLayout.astro` sets the document head with sensible defaults and accepts `title` and `description` per page.
- Adds canonical URLs, Open Graph, Twitter card metadata, and a sitemap link.
- Fonts are loaded from Adobe Typekit with `preconnect` and `preload`.

## Styling

- The design uses Tailwind CSS 4 via the Vite plugin.
- `src/styles/global.css` defines CSS variables for colors and typography, Tailwind theme tokens, and shared animations (e.g., `.fade-in`).

## Accessibility and Performance

- Lightweight Astro pages with partial hydration only where needed.
- Semantic markup for headings and navigation.
- Optimized images via `astro:assets`.

## Sitemap & Robots

- `@astrojs/sitemap` is configured in `astro.config.mjs` with `site` and `changefreq: weekly`.
- `public/robots.txt` is included.

## Deployment

- The site is production-ready and deploys well to Netlify, Vercel, or any static host.
- Ensure `site` in `astro.config.mjs` matches your production URL for correct canonical links and sitemap generation.


## Scripts

- `dev`: start local dev server
- `build`: production build
- `preview`: preview built site

## License

This portfolio is licensed under the MIT License. You are free to reuse structure and patterns; please replace content, media, and personal details with your own.
