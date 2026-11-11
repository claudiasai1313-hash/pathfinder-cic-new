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
- Framework: **Astro 5** (Wix's `headless link` does not support Astro 6).

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
