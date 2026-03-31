# NORDNOVA Website v2

Minimalist dark Scandinavian website built with **Hugo**.
Bilingual (English / Swedish), pure CSS animations, animated hamburger menu,
Josefin Sans + Martian Mono typography, dark grey + bronze palette.

---

## Quick local preview

1. [Download Hugo](https://gohugo.io/installation/) v0.136.0+ (extended edition)
2. Open a terminal in this folder
3. `hugo server`
4. Open `http://localhost:1313`

---

## Publish on Cloudflare Pages

1. Push this folder to a GitHub repository
2. Go to [pages.cloudflare.com](https://pages.cloudflare.com) → Create a project → connect your repo
3. Build settings:
   - **Build command:** `hugo --minify`
   - **Output directory:** `public`
   - **Environment variable:** `HUGO_VERSION` = `0.136.0`
4. Deploy, then add `nordnova.se` as a custom domain

Every `git push` to `main` auto-rebuilds the site.

---

## File map — what to edit and where

```
nordnova2/
│
├── config/_default/
│   ├── hugo.toml            ← Site title, contact details, social URLs
│   ├── menus.en.toml        ← English nav links
│   └── menus.sv.toml        ← Swedish nav links
│
├── content/
│   ├── en/
│   │   ├── about.md         ← About page text (EN)
│   │   ├── services.md      ← Services page title/subtitle (EN)
│   │   ├── contact.md       ← Contact page title/subtitle (EN)
│   │   └── projects/        ← One .md file per project (EN)
│   └── sv/                  ← Same structure in Swedish
│
├── data/
│   ├── home.yaml            ← Hero image path
│   ├── services_en.yaml     ← All service cards (EN) ← EDIT HERE
│   ├── services_sv.yaml     ← All service cards (SV) ← EDIT HERE
│   ├── values_en.yaml       ← Values section (EN)
│   └── values_sv.yaml       ← Values section (SV)
│
├── static/
│   ├── css/main.css         ← All styling — colours at top in :root {}
│   └── images/              ← PUT YOUR PHOTOS HERE
│       ├── logo.svg         ← Your NORDNOVA logo (already in place)
│       ├── hero.jpg         ← Home page hero image (replace placeholder)
│       └── about-placeholder.jpg
│
└── layouts/                 ← HTML templates (rarely need editing)
    ├── index.html           ← Home page
    ├── about/single.html    ← About page
    ├── services/single.html ← Services page
    ├── contact/single.html  ← Contact page
    └── projects/list.html   ← Projects listing
```

---

## Most common tasks

### Change colours
Open `static/css/main.css`, find `:root {` at the top:
```css
--bg:       #181818;   /* main page background */
--bg-mid:   #202020;   /* section backgrounds */
--bg-card:  #242424;   /* card backgrounds */
--bg-header:#141414;   /* header & footer */
--bronze:   #a07840;   /* accent colour */
--text:     #e8e4de;   /* main text */
```

### Replace the hero image
Drop your photo into `static/images/` as `hero.jpg` (1920×1080 px recommended).
That's it — the site picks it up automatically from `data/home.yaml`.

### Add/change the About photo
Put your image in `static/images/about-office.jpg`, then in
`layouts/about/single.html` find the img tag and change `src`:
```html
<img src="/images/about-office.jpg" alt="NORDNOVA office" ...>
```

### Add team photos
In `layouts/about/single.html`, find the avatar divs with initials `SA` / `KH`.
Replace `<span>SA</span>` with:
```html
<img src="/images/sam.jpg" alt="Sam Abrahamsson">
```
Put the photo in `static/images/` (recommended: 400×400 px, square crop).

### Add a service
Open `data/services_en.yaml` (and `services_sv.yaml`), copy any block and paste:
```yaml
- title: "My New Service"
  category: "Category"
  short: "Short teaser shown on home page."
  description: >
    Longer description shown on the Services page.
  features:
    - Feature one
    - Feature two
  image: ""   # or /images/service-photo.jpg
```

### Remove a service
Delete its block from both `data/services_en.yaml` and `data/services_sv.yaml`.

### Add a project
Create `content/en/projects/project-name.md`:
```markdown
---
title: "Project Title"
date: 2026-06-01
category: "Architecture"
location: "Hultsfred, Sweden"
year: 2026
image: "/images/project-photo.jpg"
draft: false
---

Description of the project here.
```
Create a matching file in `content/sv/projects/`.
Set `draft: true` to hide it; `draft: false` to show it.

### Update social media URLs
Open `config/_default/hugo.toml`:
```toml
[params]
  whatsapp  = "https://wa.me/46XXXXXXXXX"
  instagram = "https://instagram.com/nordnova"
  linkedin  = "https://linkedin.com/company/nordnova"
```

### Change contact details
Also in `config/_default/hugo.toml`:
```toml
  email_sam    = "sam@nordnova.se"
  email_khaled = "khaled@nordnova.se"
  phone_sam    = "+46 709 360 304"
  phone_khaled = "+46 709 360 295"
```

---

## Recommended image sizes

| Image | Path | Size |
|---|---|---|
| Hero photo | `static/images/hero.jpg` | 1920 × 1080 px |
| About/office | `static/images/about-placeholder.jpg` | 900 × 1200 px |
| Project photos | `static/images/project-*.jpg` | 1200 × 900 px |
| Team portraits | `static/images/sam.jpg` | 400 × 400 px |

Use JPG for photos (keep under 500 KB each). The logo is already SVG — keep it that way.

---

## Contact form

The form uses **Cloudflare Pages Forms** — free, zero backend needed.
Submissions appear in your Cloudflare dashboard under Pages → your project → Forms.

For an external service instead, edit `layouts/contact/single.html` and change
`<form action="..." method="POST">` to your provider's endpoint.
