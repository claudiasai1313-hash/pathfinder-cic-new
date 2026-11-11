# Pathfinder Healthcare Developments CIC — website redesign

A bespoke redesign of the Pathfinder CIC website, built as a Wix Headless (Wix-managed) frontend.
The owner is not an experienced developer: work step by step, explain each step in plain
language, and confirm before anything that is hard to undo.

## Hard rules

- **Never touch the live site at pathfinder-cic.com.** Do not connect, transfer or repoint that
  domain. Work only on the Wix Headless project below.
- **Never create a new Wix site.** Connect code to the existing project only. Wix CLI commands
  such as `npm create @wix/new … headless` and `init` provision a NEW site: check the Wix docs
  for how to link to the existing site before running any setup command.
- **Do not publish or release** (`wix release`, deploy, publish) without the owner's explicit
  go-ahead for that specific release.
- **Do not delete Wix content or uninstall Wix apps** without explicit approval, even content
  already marked for removal.

## Wix project

- Name: Pathfinder CIC · Site ID `3e79c66a-f963-4700-91c1-c36c7e8718c0`
- Type: Wix Headless, Wix-managed (hosted by Wix), namespace HEADLESS, no domain connected.
- Locale: en-GB, GBP, Europe/London.
- Framework: **Astro 7** with `@wix/astro` 3.x, matching Wix's current blank template. (Astro 5
  only works with the older `@wix/astro` 2.x line; the "Astro 5 only" note in Wix's docs applies to
  the `headless link` command, which we do not use because it creates a new site.)
- `wix.config.json` was written by hand (`projectType: "Site"`, `appId`, `siteId`) because every
  Wix setup command provisions a new site. Its shape matches the Wix CLI's own config schema, and
  `wix env pull` returned the same client ID. Do not change it.

## Local development

- Node **24.22.1+** is required by `@wix/cli` (`node -v` to check).
- First run on a machine: `npm install --ignore-scripts`, then `npx wix env pull` (writes
  `.env.local`, which is git-ignored and must never be committed).
- Preview locally: `npm run dev` (http://localhost:4321). Build locally: `npm run build`.
- Never run `npm run release` / `wix release` without the owner's explicit go-ahead.
- In Claude's cloud sandbox the local preview cannot fetch Wix visitor tokens (the Cloudflare
  `workerd` runtime does its own DNS and the sandbox only allows proxied traffic), so pages that
  call Wix return a 500 there. Verify Wix calls with REST + a visitor token instead, or preview on
  a normal computer. Also, Astro 7 runs `astro dev` in the background when it detects an AI agent,
  which makes `wix dev` exit; use `npx astro dev` / `npx astro dev logs` / `npx astro dev stop`.

## Scope at launch

Priorities, in order of importance to the owner:

1. A highly polished Homepage, About section and What We Do section.
2. Events and conferences — Wix Events where appropriate.
3. Reports, publications and downloadable resources.
4. Innovation, research and partnership activities.
5. Contact and enquiry forms (Wix Forms).
6. News/updates — optional, and must never dominate the site.

Out of scope at launch: online shop, paid memberships/plans, booking services.

The Wix project currently holds auto-generated sample content that is **not** genuine Pathfinder
content: 9 store products, 3 booking services, 3 blog posts, plus installed Stores, Bookings and
Paid Plans apps. Its removal is planned but **not approved yet** — do not delete it.

## Design direction

The goal is an exceptional, bespoke, art-directed website — not a standard corporate healthcare
site. Exceptional typography, thoughtful motion, intuitive navigation.

Avoid:
- generic AI-generated design and predictable layouts
- repetitive card grids
- stock healthcare photography (including the stand-in photos bundled with the Taste skill)
- unnecessary decorative elements

## Design skills (in `.claude/skills/`)

How they work together:
- **Impeccable** (`/impeccable …`): product context (`init` → PRODUCT.md, `document` → DESIGN.md),
  critique, audit and polish. Its design-check hook is configured in `.claude/settings.json`.
- **Taste** (`design-taste-frontend`): anti-generic layout and copy rules. Where Taste's
  defaults conflict with the design direction above (e.g. stand-in photography), this file wins.
- **Emil Kowalski's skills**: the authority on motion — `animate`, `choreograph`,
  `review-animations` (run manually), `find-animation-opportunities`, `animation-performance`,
  `emil-design-eng`, and related skills. Prefer the simplest tool that works (CSS before
  GSAP); always support reduced motion.

Third-party licences for these skills are in `licenses/`.

## Frontend libraries (install only once the Astro project is established)

- GSAP + ScrollTrigger — for the scroll-driven moments that genuinely need it.
- Lenis — smooth scrolling, if it proves appropriate.
- React Bits — copy individual components in and restyle them; it is not a single package.
