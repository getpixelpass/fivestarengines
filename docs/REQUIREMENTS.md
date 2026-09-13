# Five Star Engines — Feature Requirements

Living spec of what the site needs to do. Built incrementally from
screenshots and discussion. This drives the build plan — see `CLAUDE.md`
for *how* we implement anything listed here.

Status key: 🟢 confirmed requirement · 🟡 under discussion · ⚪ idea, not committed

Pages captured so far: Home, Shop/Collection, Product detail, About,
Contact, Gallery, Resources. All from the current live site
(fivestarengines) — treated as the baseline to replicate, not just
inspiration, unless noted otherwise.

---

## Global (appears on every / most pages)

- 🟢 **Header** — logo, nav (Crate Engines, Replacement Engines, About,
  Gallery, Resources, Contact), account icon, cart icon.
- 🟢 **Footer** — logo, address/phone/email, nav columns, social icons
  (Facebook, Instagram), copyright, Privacy Policy / Terms of Service
  links.
- 🟢 **Trust bar** — 2-column red banner ("100% Positive Reviews on
  eBay" / "A+ Rating with the BBB"). Identical on every page seen so
  far (home, shop, product, about, contact, gallery, resources).
  *Implementation note:* since it's identical everywhere, this is a
  candidate for Horizon's footer group (renders once, appears on every
  template automatically) rather than adding the section to each page
  individually.
- 🟢 **Bottom CTA banner** — dark background image, "Professionally-
  Built High-Performance Engines" heading, two buttons (Shop Crate
  Engines / View Replacement Engines). Also identical on every page —
  same footer-group candidate as the trust bar.
- 🟢 **Interior page banner** — background image + large heading +
  one-line subtext, used at the top of About, Contact, Gallery,
  Resources, and Shop pages (only Home has a different, bigger hero).
  One reusable section/snippet, content editable per-page.
- 🟢 **"Built Right Since 1990" mini teaser** — small image + heading +
  short paragraph + button, reused on Home and Product pages (probably
  elsewhere too). Links to About page.

## Testimonials

- 🟢 **Customer testimonials** — reused on Home, Shop, and Product
  pages. Each testimonial: 5-star rating, quote, and a product name
  label (e.g. "Ford 351 Windsor 345 HP Turn-Key High Performance
  Balanced Crate Engine") — the label is descriptive text, not
  necessarily a live product link.
  Custom section (`pp-testimonials`) with repeatable blocks (quote,
  star count, product label) so merchant can add/edit/reorder without
  touching code.
  ❓ Open question: hand-entered by merchant, or pulled from a review
  app (Yotpo/Judge.me/Loox)? Affects build approach significantly.

## Product catalog & product cards

- 🟢 **"Bestseller" badge** on product card thumbnails — seen on Home,
  Shop grids, and even a cross-sell item on the Product page (spark
  plugs). *Likely implementation:* a Shopify product tag (e.g.
  `bestseller`) checked in the shared product-card snippet.
  ❓ Should badge support other types later (New, Sale, Low Stock), or
  is "Bestseller" the only one for now? Affects whether we build a
  single tag check or a small badge-priority system.
- 🟢 **Star rating on product cards** — shown as stars + a count in
  parentheses, e.g. "★★★★☆ (4)". ❓ Where does this come from — a
  review app, or a manually-set metafield (average + count) with no
  full review system behind it? This decides a lot (app integration vs.
  two simple metafields).
- 🟢 **Spec line on product cards** — 3 key stats shown per card
  (varies slightly by page: Home/Shop show Horsepower + Application/
  Fitment + Warranty). Backed by product metafields, rendered in the
  card snippet.
- 🟢 **"View Product" CTA** on every card.

## Shop / Collection page

- 🟢 **Filter sidebar**, collapsible groups, checkboxes:
  - Make (Chevrolet, Ford, …)
  - Engine Size (283, 302, 327, 350, 351W, 383, 454, …)
  - Horsepower (ranges: <300, 300–349, 350–399, 400+)
  - Engine Package (Balanced, Turn-Key, TBI, Vortec, Aluminum Heads)
  - Vehicle Type (Truck, Mustang, Camaro, RV/Van, 4x4)
  - Price Range (Under $4,000, $4,000–$4,999, $5,000–$5,999, $6,000+)
  *Likely native:* Shopify's built-in Search & Discovery filtering,
  which Horizon supports out of the box, driven by product metafields/
  options for each of the above facets. This is a metafield-setup and
  configuration task, not custom filtering code.
- 🟢 Product grid using the shared product card (badge, rating, specs,
  price, View Product).
- Reused globals below the grid: testimonials, "Built Right" teaser,
  trust bar, CTA banner.

## Product detail page

- 🟢 **Breadcrumb** back to the collection ("← Back to All Crate
  Engines").
- 🟢 **Media gallery** with thumbnails — native Horizon product media.
- 🟢 **Price + rating** (see product catalog section above re: rating
  source).
- 🟢 **Financing widget** — "Starting at $224/mo with Affirm — See if
  you qualify." ❓ Decision needed: Shopify's native Shop Pay
  Installments vs. an Affirm app integration. Affects setup but not
  theme code much either way (both typically drop in as a snippet/
  script near price+ATC).
- 🟢 **Add to Cart** — native Shopify cart.
- 🟢 **"Want to customize this engine? Click here to reach out to our
  team"** — a callout banner on the PDP linking to the Contact page.
  Likely a simple conditional block/setting on the product template
  (maybe only shown for certain products/tags).
- 🟢 **Details** — rich text product description (native).
- 🟢 **Spec table** — Engine Platform, Horsepower, Package Type,
  Application, Balanced Assembly, Warranty. Structured key/value data
  → product metafields rendered via a spec-table snippet (reusable
  across all engine products regardless of which specs are filled in).
- 🟢 **Features — two-column bullet lists**: "New parts include" and
  "Five Star professional machine work on engine includes." Likely two
  rich-text/list metafields (or two blocks), varies per product.
- 🟢 **Recommended Add-ons** — curated cross-sell products (e.g. oil
  kit, spark plugs, gaskets) shown as a small product grid with badges/
  ratings/price/Add to Cart. ❓ Manually curated per-product (product-
  list metafield referencing specific products) vs. Shopify's
  algorithmic product recommendations API? The examples shown look
  hand-picked (oil + plugs + gaskets — accessories, not similar
  engines), which points toward manual curation.
- 🟢 **Contact info bar** — black banner with phone/hours/email,
  specific to the Product page in what we've seen so far (not
  confirmed on other pages).
- Reused globals below: "Built Right" teaser, trust bar, CTA banner.

## About page

- 🟢 **Page banner** (reused pattern).
- 🟢 **"Who We Are"** — stacked image column (3 photos) + rich text
  bio (multiple paragraphs) + signature line ("Chris Smith, Owner").
  Straightforward media-with-content pattern, likely native Horizon
  section configured with our copy.
- 🟢 **"Watch Our Story"** — large video block with custom play-button
  overlay on a poster image. ❓ Hosted where — native Shopify video,
  YouTube, or Vimeo? Affects whether this is Horizon's native video
  section (if Shopify-hosted) or a custom embed block.
- 🟢 **"Meet [Team Member]"** bio section — dark background, centered
  text bio, plus a row of video thumbnails (styled like an external
  "Ask Ed" video series/channel) each with title text overlaid on the
  thumbnail image and presumably linking out to the video.
  *Recommended approach:* simple custom blocks (thumbnail image, title
  text, link URL) rather than a live YouTube API integration — avoids
  needing API keys for what's essentially 3 curated links.
  ❓ Confirm: just link out to YouTube on click, or should it open an
  inline player?

## Contact page

- 🟢 **Page banner** (reused pattern).
- 🟢 **"Get in Touch" card** — phone number and email as tap/click
  buttons (`tel:` / `mailto:` links).
- 🟢 **"Find Us" card** — address + "Get Directions" button (links out
  to Google/Apple Maps with the address).
- 🟢 **"Hours" card** — static business hours text.
- 🟢 **Contact form** — Full Name*, Phone Number*, Email, message*,
  Submit. *Native Shopify feature* — use Shopify's built-in contact
  form (`{% form 'contact' %}`), which emails the store's Contact
  notification address; no custom backend needed.
- 🟢 **Embedded map** — Google Maps iframe showing the shop location.

## Gallery page

- 🟢 **Page banner** (reused pattern).
- 🟢 **Photo grid** (2-column) of past project photos.
- 🟢 **"Load More" pagination** — grid loads additional photos in
  batches rather than showing everything at once.
  ❓ Decision: a metaobject-based photo list (merchant can add new
  project photos anytime without dev help — recommended if this grows
  regularly) vs. a simpler blocks-in-a-section approach with a "show
  more" JS reveal (simpler to build, fine if photos are added
  infrequently). Depends how often new gallery photos get added.

## Resources page

- 🟢 **Page banner** (reused pattern).
- 🟢 **Resource card grid** (2×2 seen, likely expandable) — each card:
  title + "View" button linking out to a document/PDF or a resource
  page. Examples seen: Parts Removal List, Engine Color Chart, Engine
  Break-In Procedure, Crate Engine Break-In Procedure.
  *Recommended approach:* a custom section with repeatable blocks
  (title, button label, link/file) — simple, merchant-editable, no
  need for a metaobject given the small, slow-growing count.

## Open questions to resolve

1. Testimonials: hand-entered by merchant, or from a review app?
2. Product ratings: review app, or manual metafield (average + count)?
3. Badges: "Bestseller" only, or more types planned (New, Sale, Low
   Stock)?
4. Financing: Shop Pay Installments (native) or Affirm app?
5. Recommended Add-ons: manually curated per product, or Shopify's
   algorithmic recommendations?
6. "Watch Our Story" video: Shopify-hosted, YouTube, or Vimeo?
7. "Meet Ed Smith" video thumbnails: link out on click, or inline
   player?
8. Gallery: metaobject-based (scales better) or simple blocks (simpler,
   fine for occasional updates)? How often do new photos get added?
9. Contact info bar (black banner with phone/hours) — Product page
   only, or should it appear elsewhere too?
