# Fatin's Portfolio Website

Personal portfolio for **Nurul Fatin Amira Binti Mohd Riza** — Data Engineer.

**Live URL:** `https://watnoffin.github.io/fatin-webportfolio/`

Built with [Astro](https://astro.build/) + TypeScript + [Tailwind CSS v4](https://tailwindcss.com/), deployed as a fully static site to GitHub Pages.

---

## Why this stack?

| Concern | Choice | Reason |
|---|---|---|
| Framework | Astro | Zero JS by default; static output; great DX; MDX support |
| Styles | Tailwind CSS v4 | Utility-first; tiny CSS output; dark mode via class strategy |
| Content | JSON + MDX | Edit text without touching components; add a project by adding one file |
| Hosting | GitHub Pages | Free; custom domain support; CI deploys on push |
| Fonts | Plus Jakarta Sans + Inter | Distinctive heading font + highly legible body font |

---

## Running locally

```bash
# Prerequisites: Node 18+, npm 9+
cd portfolio-web
npm install
npm run dev
```

Open `http://localhost:4321/portfolio-web/` in your browser. The site hot-reloads on every save.

### Other commands

```bash
npm run build      # Production build → dist/
npm run preview    # Serve the dist/ output locally
npm run astro check  # TypeScript / type check
```

---

## Editing content

All content lives in `src/content/`. You never need to touch any component to update text.

### Edit your bio, tagline, email, or social links

Open `src/content/site.json` and change the relevant fields.

### Add or edit a work experience entry

Open `src/content/experience.json`. Each entry follows this shape:

```json
{
  "id": "my-company",
  "role": "Job Title",
  "company": "Company Name",
  "location": "Malaysia",
  "startDate": "January 2025",
  "endDate": null,
  "current": true,
  "highlights": [
    "What you did in plain English."
  ]
}
```

Set `"current": true` and `"endDate": null` for your present role.

### Add or edit a skill category

Open `src/content/skills.json`. Add a new object with `"category"` and `"skills"` array.

### Add a certification

Open `src/content/certifications.json`. Use `"icon": "aws"`, `"ibm"`, or `"oracle"` for the coloured badge.

### Add a new project

1. Create a new file: `src/content/projects/my-project-slug.mdx`
2. Add the frontmatter (copy from an existing file and change the values).
3. Add the project to the projects array inside `src/components/sections/Projects.astro` (the cards on the home page).
4. Add the project slug, content, and SVG diagram to `src/pages/projects/[slug].astro` — look for the `contents` and `diagrams` records.

> **Tip:** The slug in the filename, in the Projects component, and in `[slug].astro` must all match.

---

## Swapping the profile photo

In `src/components/sections/Hero.astro`, find the `TODO(owner)` comment and replace the initials `<div>` with:

```html
<img
  src="/portfolio-web/photo.webp"
  alt="Nurul Fatin Amira Binti Mohd Riza — profile photo"
  class="relative w-64 h-64 lg:w-80 lg:h-80 rounded-full object-cover border-4 border-white dark:border-gray-800 shadow-2xl"
  width="320"
  height="320"
/>
```

Place your photo file at `public/photo.webp` (WebP recommended for performance; ~100–200 KB).

---

## Swapping the CV PDF

Replace `public/cv.pdf` with your actual CV PDF. The filename must remain `cv.pdf`.

---

## Deployment — GitHub Pages

### First-time setup

1. Push this repository to GitHub (your account, repo name `portfolio-web`).
2. Go to **Settings → Pages → Source** and select **GitHub Actions**.
3. The workflow at `.github/workflows/deploy.yml` runs automatically on every push to `main`.
4. After the first successful run, your site will be live at:
   `https://<your-github-username>.github.io/portfolio-web/`

> The `astro.config.mjs` already has `site: 'https://watnoffin.github.io'` and `base: '/portfolio-web/'` configured.

### Custom domain (optional)

1. Buy a domain (e.g. `fatin.dev`).
2. Add a `CNAME` file to `public/` containing just your domain: `fatin.dev`
3. In GitHub → Settings → Pages → Custom Domain, enter your domain.
4. Update `astro.config.mjs`: set `site: 'https://fatin.dev'` and `base: '/'`.
5. Update `robots.txt` sitemap URL to match.
6. Follow your DNS provider's instructions to add an `A` record pointing to GitHub's IPs or a `CNAME` to `watnoffin.github.io`.

### Alternative: Vercel / Netlify

Both support Astro out of the box. Connect your repo, set build command to `npm run build`, and output directory to `dist`. Remove or change the `base` config if deploying to root.

---

## Dark mode

Dark mode follows the system setting automatically. A manual toggle (moon/sun icon in the nav) lets visitors override it. The preference is saved to `localStorage`.

The `dark:` Tailwind classes and a `<script is:inline>` in `BaseLayout.astro` prevent flash-of-unstyled-content (FOUC).

---

## Accessibility

- WCAG 2.1 AA colour contrast throughout (violet on white: 5.3:1+)
- `<skip-link>` for keyboard navigation
- All images and decorative SVGs use `aria-hidden="true"` or `alt` text
- All interactive elements have visible focus rings via `:focus-visible`
- `aria-label` / `aria-labelledby` on every section and landmark
- Lists use `role="list"` where CSS removes default list styling
- Animated elements respect `prefers-reduced-motion`

---

## SEO

Each page has:
- `<title>` and `<meta name="description">`
- Open Graph tags (`og:title`, `og:description`, `og:image`)
- Twitter Card tags
- JSON-LD `Person` structured data on all pages
- Sitemap at `/portfolio-web/sitemap-index.xml` (generated by `@astrojs/sitemap`)
- `robots.txt` at `/portfolio-web/robots.txt`

The Open Graph image (`public/og-image.png`) is an SVG-as-PNG placeholder. **TODO(owner):** Replace with a real 1200×630 PNG for best social sharing previews.

---

## Privacy notes

- No phone number or street address is published.
- Work project case studies are written at a conceptual level only — no internal server names, hostnames, tool configurations, or document names.
- References line: "Available upon request."
- No analytics by default. To add Plausible or Umami, add their one-line script in `BaseLayout.astro` behind an env-flag.

---

## TODO(owner) checklist

The following items still need your input:

- [ ] **Profile photo** — add `public/photo.webp` and update `Hero.astro` (see instructions above)
- [ ] **CV PDF** — replace `public/cv.pdf` with your actual CV
- [ ] **OG image** — replace `public/og-image.png` with a real 1200×630 PNG for social previews
- [ ] **Project screenshots** (optional) — if you want to show visuals on case-study pages, add images to `public/projects/` and reference them in `[slug].astro`
- [ ] **Metrics / quantitative outcomes** (optional) — if you're comfortable publishing any numbers (e.g. "reduced report generation time by X%"), add them to the relevant project content in `[slug].astro`
- [ ] **Custom domain** — if/when you get one, follow the custom domain section above and update `astro.config.mjs`
- [ ] **GitHub repo visibility** — make the repo public so GitHub Pages can serve it on a free plan

---

## File structure

```
portfolio-web/
├── public/                  # Static assets served as-is
│   ├── cv.pdf               # ← Replace with real CV
│   ├── favicon.svg
│   ├── og-image.png         # ← Replace with real OG image
│   └── robots.txt
├── src/
│   ├── content/             # ← All text content lives here
│   │   ├── site.json        # Name, email, social links, tagline
│   │   ├── experience.json  # Work history
│   │   ├── skills.json      # Skill categories
│   │   ├── certifications.json
│   │   ├── education.json
│   │   ├── leadership.json
│   │   └── projects/        # One MDX file per project (not used for rendering yet — see [slug].astro)
│   ├── components/
│   │   ├── Navbar.astro
│   │   ├── Footer.astro
│   │   └── sections/        # One component per home page section
│   ├── layouts/
│   │   ├── BaseLayout.astro  # HTML shell, meta tags, dark mode
│   │   └── PageLayout.astro  # Navbar + main + footer wrapper
│   ├── pages/
│   │   ├── index.astro       # Home page
│   │   ├── 404.astro
│   │   └── projects/
│   │       └── [slug].astro  # Dynamic project case-study pages
│   └── styles/
│       └── global.css        # Design tokens, base styles, animations
├── .github/workflows/
│   └── deploy.yml            # GitHub Pages CI/CD
├── astro.config.mjs
├── package.json
└── tsconfig.json
```
