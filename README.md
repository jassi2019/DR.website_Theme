# Dr. Kathuria's Dentistry — Website

A premium, mobile-optimized website for **Dr. Kathuria's Dentistry** (East of Kailash, New Delhi) built with pure HTML, CSS, and vanilla JavaScript. Designed for international dental tourism patients with a focus on luxury aesthetics, fast load times, and zero-dependency simplicity.

**Live URL:** https://dr-kathuria-dentistry.netlify.app

---

## Tech Stack

- **HTML5** — Semantic markup, multi-page (5 pages)
- **CSS3** — Custom properties, flex/grid, responsive (mobile-first)
- **Vanilla JavaScript** — No frameworks, no build step
- **Font Awesome 6.5** — Icons (CDN)
- **Google Fonts** — Cormorant Garamond + DM Sans
- **Netlify** — Hosting, CDN, SSL, Forms
- **Unsplash** — Stock imagery (CDN)

> **No build process. No npm install required.** Just open `index.html` in a browser to develop locally.

---

## Project Structure

```
dental-delhi/
├── index.html              # Homepage (hero, services, testimonials, smile quiz, etc.)
├── about.html              # About us — doctors, clinic, certifications, journey
├── services.html           # All 50+ treatments grouped by category
├── cases.html              # Before/After case gallery with filters
├── contact.html            # Contact form, map, location, video consult
│
├── css/
│   └── style.css           # All styles (~1500 lines, well-commented sections)
│
├── js/
│   └── main.js             # All interactivity — sliders, modals, forms, quiz
│
├── netlify.toml            # Netlify build config (form processing enabled)
└── README.md               # You are here
```

---

## Brand Design System

### Color Palette (matches delhidental.com)

| Token        | Hex       | Usage                          |
|--------------|-----------|--------------------------------|
| `--gold`     | `#bea657` | Primary brand (CTAs, accents)  |
| `--gold-l`   | `#d4ad55` | Lighter gold (hovers)          |
| `--gold-xl`  | `#f0cc7a` | On dark backgrounds            |
| `--ink`      | `#0b1220` | Near-black (footer, dark UI)   |
| `--navy`     | `#0d1f3c` | Deep navy (info bars)          |
| `--teal`     | `#00a8c0` | Secondary (legacy)             |
| Body text    | `#2b2b2b` | Charcoal (delhidental brand)   |
| Cream border | `#f4e8ca` | Subtle dividers                |

### Typography

- **Headings:** `Cormorant Garamond` (serif, editorial luxury feel)
- **Body / UI:** `DM Sans` (clean modern sans-serif)
- Italic emphasis (`<em>`) is gold-colored throughout

### Spacing & Tokens

CSS custom properties defined in `:root` block at the top of `style.css`:

```css
:root {
  --nav-h:   76px;       /* Navbar height (responsive) */
  --r-sm:    6px;        /* Border radius small */
  --r-md:    12px;
  --r-lg:    20px;
  --shadow-l: 0 20px 70px rgba(11,18,32,.18);
  --ease:    cubic-bezier(.4,0,.2,1);
}
```

---

## Key Features

### Homepage Sections (in order)

1. **Premium Navbar** — Gold tooth logo, gradient bottom border, animated CTA pill button
2. **Hero Slider** — 3 cinematic full-screen slides with parallax + auto-advance
3. **Info Bar** — 3 quick-fact tiles (rating, phone, hours)
4. **Ticker Marquee** — Scrolling certifications & global numbers
5. **Stats Strip** — Animated counters (15K+ patients, 44+ countries, etc.)
6. **About Preview** — 2-column with overlapping image badge
7. **Services Grid** — 6 treatment cards with images, prices, badges
8. **Why Choose Us** — Feature list with icon items
9. **Before/After Slider** — Drag-to-compare image reveal (custom JS)
10. **How It Works** — 4-step journey
11. **Testimonials Carousel** — International patient reviews with avatars
12. **Celebrity Smiles** — VIP grid with hover overlays
13. **Video Consultation** — Teledentistry CTA with phone numbers
14. **Advanced Technology** — 4-card tech showcase (CEREC, microscope, etc.)
15. **Google Reviews** — 3-card review widget with badge
16. **Countries Band** — Big "44+" stat with country pill cloud
17. **Smile Confidence Score Quiz** — Interactive 5-question quiz with animated SVG ring + personalized treatment recommendations
18. **Clinic Gallery** — 8-image masonry grid with lightbox
19. **Instagram Feed** — 6-tile grid with overlay
20. **Final CTA Banner** — Gradient strip with WhatsApp + booking
21. **Footer** — 4-column grid with treatments, links, contact, brand

### Floating Action Buttons (FAB)

- **Gold Call button** (bottom-left) — opens phone dialer with toll-free number
- **Green WhatsApp button** (bottom-right) — opens WhatsApp chat
- **Scroll-to-top** (above WhatsApp) — appears after 400px scroll

### Side Contact Strip (Desktop)

Vertical column on left edge (hidden on mobile, replaced by FABs):
- Phone (Navy) → tap to call
- WhatsApp (Green)
- Instagram (Pink)
- Facebook (Blue)
- YouTube (Red)

Each button is icon-only (44px), expands to 160px on hover revealing the label.

### Floating Booking Modal

- Triggered by any "Book Free Consult" / "Book Appointment" button
- Slides in from right (desktop) or up from bottom (mobile)
- Form integrates with **Netlify Forms** for spam-protected submissions
- AJAX submit (no page reload), shows toast on success
- Honeypot field for bot protection

---

## Forms & Email Notifications

The booking form uses **Netlify Forms** (free tier — 100 submissions/month).

**Form name:** `appointment`
**Fields:** name, country, phone, email, treatment (select), message

### Email Setup

A notification hook is configured to forward every submission to the admin email. To change the recipient:

```bash
# 1. Get the form ID
netlify api listSiteForms --data='{"site_id":"YOUR_SITE_ID"}'

# 2. List existing hooks
netlify api listHooksBySiteId --data='{"site_id":"YOUR_SITE_ID"}'

# 3. Update or create the hook
netlify api createHookBySiteId --data='{
  "site_id":"YOUR_SITE_ID",
  "body":{
    "form_id":"YOUR_FORM_ID",
    "type":"email",
    "event":"submission_created",
    "data":{"email":"new@admin.com"}
  }
}'
```

Submissions are also viewable at: `https://app.netlify.com/projects/YOUR_SITE/forms`

---

## Local Development

```bash
git clone https://github.com/jassi2019/DR.website_Theme.git
cd DR.website_Theme

# Option 1: Open directly
start index.html             # Windows
open index.html              # macOS

# Option 2: Use any static server (recommended)
npx serve .                  # Opens on http://localhost:3000
# OR
python -m http.server 8000   # Opens on http://localhost:8000
```

No `npm install` needed. No build step. Just edit and refresh.

---

## Deployment (Netlify)

### Initial Setup

```bash
# Install Netlify CLI globally
npm install -g netlify-cli

# Login (opens browser)
netlify login

# Deploy from this folder (creates a new site on first run)
netlify deploy --dir=. --prod
```

### Subsequent Deploys

```bash
netlify deploy --dir=. --prod
```

Deploys typically take 5-10 seconds. Free tier includes:
- 100GB/month bandwidth
- Free SSL/HTTPS
- Global CDN
- 100 form submissions/month
- Unlimited static sites

### Custom Domain

To attach a real domain (e.g., `drkathuriadentistry.com`):

1. Buy domain from Hostinger / GoDaddy / Namecheap (~₹99–999/year)
2. In Netlify dashboard → **Domain management** → **Add custom domain**
3. Update DNS at registrar:
   - `A` record → `75.2.60.5`
   - `CNAME` (www) → `dr-kathuria-dentistry.netlify.app`
4. Netlify auto-provisions Let's Encrypt SSL within minutes

---

## Responsive Breakpoints

The CSS uses three main breakpoints:

| Width        | Target            | What Changes                                     |
|--------------|-------------------|--------------------------------------------------|
| `≤ 1200px`   | Tablets / laptops | Nav links shrink, phone label hides              |
| `≤ 1100px`   | Small laptops     | Footer 4→2 cols, steps 4→2 cols                 |
| `≤ 960px`    | Tablets           | Hamburger menu activates, grids 4→2             |
| `≤ 700px`    | Phones            | Single column, side-contact hidden, FABs shown  |
| `≤ 420px`    | Small phones      | Logo shrinks, hero h1 caps at 1.85rem           |

Important: `html` and `body` both have `overflow-x: hidden` to prevent horizontal scroll on mobile.

---

## JavaScript Architecture

`js/main.js` is a single ~350-line file with clearly commented sections:

```
PAGE LOADER          — Hides spinner on window.load
CURSOR GLOW          — (disabled on mobile)
STICKY NAV           — Adds .scrolled class on scroll
HAMBURGER            — Mobile menu toggle
HERO SLIDER          — Auto-advance + manual dots/arrows
BEFORE/AFTER         — Drag-to-compare with mouse + touch events
TESTIMONIAL CAROUSEL — Translate-X based slider
STAT COUNTERS        — IntersectionObserver triggers count-up
REVEAL ANIMATIONS    — IntersectionObserver adds .is-visible
LIGHTBOX             — Click image → fullscreen modal
FORM SUBMIT          — AJAX to Netlify, toast on success
TOAST                — Bottom-right notification
SMOOTH SCROLL        — For all #anchor links
FILTER TABS          — For Cases page category filtering
ACTIVE NAV LINK      — Highlights current page in nav
FAB SCROLL TO TOP    — Shows after 400px scroll
SMILE SCORE QUIZ     — Multi-step quiz with score ring + result
```

No external JS dependencies. No frameworks. No bundler.

---

## Browser Support

- Chrome/Edge (latest 2 versions) ✅
- Safari 14+ ✅
- Firefox (latest 2) ✅
- iOS Safari 14+ ✅
- Android Chrome 90+ ✅
- IE11: **not supported** (uses CSS custom properties, grid, flexbox)

---

## Performance Notes

- **No build step** — fewer moving parts, faster iteration
- **CDN images** (Unsplash) — lazy-loaded by browser
- **Single CSS file** — one HTTP request after Font Awesome
- **Single JS file** — one HTTP request, deferred
- **System fonts as fallback** — text renders before web fonts load
- **Netlify CDN** — global edge caching, ~50ms TTFB worldwide

For production: consider self-hosting Unsplash images and converting to WebP for ~40% smaller file sizes.

---

## Common Edits

### Change phone number

Search & replace across all HTML files:
- `1800-11-7272` (toll-free)
- `+91 98109 36360` (WhatsApp)
- `tel:18001177272` (links)
- `wa.me/919810936360` (WhatsApp links)

### Change brand color

Edit `:root` block in `css/style.css`:

```css
:root {
  --gold:    #bea657;   /* ← change this */
  --gold-l:  #d4ad55;
  --gold-xl: #f0cc7a;
}
```

All gold UI updates automatically.

### Add a new service card

In `index.html`, find the `srv-grid-3` block and copy any `.srv-card` div. Update image, title, description, price.

### Update hero slides

In `index.html`, the `.hero-wrap` block has 3 `.hs-slide` divs. Each has its own image + heading + buttons. Add a 4th slide and a matching `<button class="hs-dot">` to the dots row.

---

## Credits

- **Client:** Dr. Sween Kathuria & Dr. Puneet Kathuria, Dr. Kathuria's Dentistry
- **Design Reference:** delhidental.com
- **Stock Images:** Unsplash
- **Icons:** Font Awesome
- **Fonts:** Google Fonts (Cormorant Garamond, DM Sans)

---

## License

Proprietary — © 2024 Dr. Kathuria's Dentistry / U and K Oral Wellness LLP.
Code contributed by the development team for client use only.
