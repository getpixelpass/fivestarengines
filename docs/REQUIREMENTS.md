# Five Star Engines — Feature Requirements

Living spec of what the site needs to do. Built incrementally from
screenshots and discussion. This drives the build plan — see `CLAUDE.md`
for *how* we implement anything listed here.

Status key: 🟢 confirmed requirement · 🟡 under discussion · ⚪ idea, not committed

For each feature: what it does, where it shows up, and how it likely
gets built (native Horizon config, Shopify native feature, or custom
`pp-` component).

---

## Global

*(nothing captured yet)*

## Home page

*(see homepage screenshot already reviewed — hero, feature grid, product
grid, testimonials, story section, trust bar, CTA banner, contact bar.
Will formalize into rows here once we lock the section list.)*

## Collection / Shop page

- 🟡 **Advanced filtering** — filter products (likely by fitment,
  engine type, power output, price, availability). *Likely native*:
  Shopify's built-in Search & Discovery filtering, which Horizon
  supports out of the box — probably a configuration/metafield task,
  not custom code. Need to confirm which attributes should be
  filterable.

## Product page / product cards

- 🟡 **"Bestseller" badge on product thumbnail** — a tag shown on the
  product image in grid/card views (collection grids, featured product
  grids, search results). *Likely implementation*: a Shopify product
  tag (e.g. `bestseller`) checked in the product card snippet to
  conditionally render a badge — avoids a manual per-product toggle
  and works everywhere the card is reused. Alternative: a metafield if
  we want more badge types later (e.g. "New", "Sale") rather than a
  single fixed tag.

## Testimonials

- 🟢 **Customer testimonials section** — star rating, quote, product
  name per testimonial (seen on homepage). Custom section
  (`pp-testimonials`) with repeatable blocks so merchant can add/edit/
  reorder testimonials in the Theme Editor without code changes.

## Open questions to resolve as we go

- Which product attributes should be filterable on the shop page?
- Should badges support more types than "Bestseller" (Sale, New, Low
  Stock)?
- Are testimonials manually entered by the merchant, or pulled from an
  external review app (e.g. Yotpo, Judge.me)? Affects whether this is
  custom-built or an app integration.
