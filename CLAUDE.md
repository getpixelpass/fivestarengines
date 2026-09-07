# Shopify Theme Development Instructions for Claude

You are helping me build a custom Shopify theme for a client.

The theme is based on Shopify Horizon and will eventually be transferred
to the client. Treat this as a production-quality commercial Shopify
theme, not a prototype.

Follow these rules throughout the entire project.

## Shopify architecture

Use Shopify's current theme architecture and Horizon conventions.

Prefer: - Liquid - HTML - CSS - Vanilla JavaScript - Shopify sections -
Shopify theme blocks - Snippets - JSON templates - Shopify
metafields/metaobjects when appropriate

Do not introduce React, Vue, jQuery, Tailwind, Bootstrap, or other
frameworks unless I specifically request them.

Do not rebuild functionality that Shopify already provides natively.

Preserve Shopify compatibility with: - Theme Editor - Shopify Markets -
localization - product variants - dynamic checkout - cart
functionality - app blocks - metafields - accessibility features

## Do not unnecessarily modify Horizon core files

Treat Horizon as the foundation.

Avoid making large edits to Shopify's original Horizon components unless
absolutely necessary.

Whenever practical, create new custom components instead of heavily
modifying existing Horizon files.

Prefix custom components with:

`pp-`

Examples:

``` text
sections/pp-hero.liquid
sections/pp-feature-grid.liquid
sections/pp-product-showcase.liquid

blocks/pp-feature-card.liquid
blocks/pp-icon-text.liquid

snippets/pp-product-badge.liquid

assets/pp-theme.css
assets/pp-theme.js
```

This makes it easy to distinguish our custom code from Shopify's
original theme code.

## Build reusable components

Do not hardcode page content directly into Liquid.

Anything the merchant may reasonably want to change later should be
editable through Shopify's Theme Editor.

Examples include: - headings - paragraphs - images - videos - button
labels - button URLs - colors - spacing - alignment - layout - number of
columns - image position - section width - mobile layout - section
visibility

Use section settings and theme blocks appropriately.

Use blocks when content should be repeatable, reorderable, removable, or
reusable.

Do not create hundreds of unnecessary settings. Only expose settings
that make sense for the merchant to control.

## Use theme blocks where appropriate

Because Horizon supports Shopify theme blocks, prefer theme blocks for
modular content.

For example, a custom hero section might allow:

``` text
Hero
- Heading
- Text
- Button
- Button
- Image
- Badge
```

The merchant should be able to reorder or remove appropriate elements
through the Theme Editor without requiring code changes.

Do not force everything into a single giant section schema.

## Keep sections independent

Sections should not depend unnecessarily on other sections.

Avoid global CSS selectors that accidentally affect unrelated
components.

Scope custom section styling appropriately.

When possible, components should work when moved to different templates.

## CSS rules

Write clean, maintainable CSS.

Prefer CSS custom properties for configurable values.

Avoid excessive use of: - `!important` - deeply nested selectors -
absolute positioning - arbitrary pixel offsets - duplicated styles

Use responsive CSS intentionally.

Build mobile-first where practical.

Always test layouts conceptually at: - mobile - tablet - desktop - large
desktop

Do not make desktop layouts that simply collapse poorly on mobile.

Reuse Horizon's existing design tokens and CSS variables when
appropriate instead of creating duplicate systems.

## JavaScript rules

Use JavaScript only when necessary.

Prefer native browser functionality and Shopify's existing functionality
before adding custom JavaScript.

JavaScript should: - be modular - avoid polluting the global scope -
work when sections are dynamically reloaded in the Shopify Theme
Editor - avoid unnecessary dependencies - avoid blocking page rendering

When JavaScript is tied to a section, make sure it still initializes
correctly when Shopify reloads that section inside the Theme Editor.

Do not attach duplicate event listeners.

## Performance

Performance matters.

Avoid: - unnecessary JavaScript - giant libraries - excessive DOM
elements - unnecessary animations - oversized images - duplicate
assets - render-blocking resources

Use Shopify image filters and responsive images correctly.

Provide appropriate image widths and `srcset` behavior.

Use lazy loading for below-the-fold images where appropriate.

Do not lazy-load critical above-the-fold hero imagery if doing so hurts
LCP.

## Product functionality

Never hardcode product information that Shopify already exposes
dynamically.

Use Shopify product objects for: - title - price - compare-at price -
media - variants - inventory - availability - product options - selling
plans

Preserve compatibility with products that have: - one variant - many
variants - unavailable variants - subscription options - multiple
product media types

Do not assume every product has the same options.

## Cart functionality

Preserve Shopify's native cart architecture whenever possible.

Do not create a completely separate cart system unless I specifically
ask for one.

When creating AJAX functionality, use Shopify's supported cart endpoints
and maintain compatibility with Horizon's existing cart behavior.

Do not duplicate cart state in unnecessary custom JavaScript.

## Accessibility

Accessibility is required.

Use: - semantic HTML - proper heading hierarchy - real button elements
for actions - real links for navigation - alt text support - keyboard
navigation - visible focus states - ARIA only when necessary

Do not make clickable divs.

Interactive elements must work with keyboard controls.

Respect `prefers-reduced-motion` for significant animations.

## SEO

Preserve Shopify's SEO functionality.

Use semantic HTML.

Do not hardcode: - canonical URLs - product structured data - metadata
already generated by Shopify

Maintain proper heading hierarchy.

Only one primary H1 should normally exist on a page unless there is a
legitimate semantic reason otherwise.

## Theme Editor experience

Always think about what happens after the site is handed to the client.

The merchant should be able to update normal website content without
contacting a developer.

Each custom section should have: - a clear section name - understandable
setting names - logical setting groups - reasonable defaults - useful
presets when appropriate

Do not expose technical terminology to the merchant unless necessary.

For example use:

`Section spacing`

rather than:

`CSS padding-bottom variable`

## Schema

Keep Shopify section schema organized.

Use clear IDs and labels.

Avoid changing setting IDs after they have been used because doing so
can wipe existing Theme Editor configuration.

Once a setting ID is established, treat it as persistent.

## File organization

Do not put the entire custom theme into one huge CSS or JavaScript file.

Keep custom functionality logically organized.

Use snippets for repeated markup.

Use blocks for reusable editor components.

Use sections for page-level components.

Avoid copy-pasting the same Liquid markup across multiple files when a
snippet would make more sense.

## Avoid overengineering

Choose the simplest solution that fits Shopify's native architecture.

Do not create abstraction layers just because they are possible.

Before creating custom functionality, ask:

1.  Does Shopify already provide this?
2.  Does Horizon already provide this?
3.  Could this be accomplished with a section setting?
4.  Could this be accomplished with a theme block?
5.  Is custom JavaScript actually necessary?

Prefer the simplest maintainable solution.

## Git safety

Do not make unrelated changes to files when completing a task.

Before changing an existing file, understand what it currently does.

When making significant changes, tell me which files you intend to
modify.

Do not delete working functionality unless I explicitly request it or it
is clearly being replaced.

Avoid large automated rewrites of existing Horizon files.

Keep changes small enough that they can be reviewed and committed
logically.

## When I provide a design

When I provide a Figma design, screenshot, or reference website:

Do not simply create a visually similar static page.

Translate the design into reusable Shopify components.

Determine: - which parts should be sections - which parts should be
blocks - which content should be merchant-editable - which elements
should be dynamic Shopify data - how the layout behaves responsively

Match the design closely while still respecting Shopify architecture.

Do not sacrifice maintainability just to reproduce a screenshot.

## Before coding a large feature

For substantial components, briefly tell me: - which files you plan to
create - which files you plan to modify - which Shopify objects/settings
will be involved - whether JavaScript is required

Then implement it.

For small fixes, you can make the change directly.

## After implementing a feature

Briefly tell me: - what you changed - which files changed - any new
Theme Editor settings - anything I should test

Do not give long explanations unless I ask.

## General rule

Whenever there is a choice between:

**A quick hack that visually works**

and

**A clean Shopify-native implementation that is reusable and editable
through the Theme Editor**

choose the clean Shopify-native implementation.

The final theme should be something another experienced Shopify
developer could open later and easily understand.
