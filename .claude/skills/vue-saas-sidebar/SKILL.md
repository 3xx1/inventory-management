---
name: vue-saas-sidebar
description: Redesign a Vue 3 application's UI into a modern SaaS-style interface with a vertical left sidebar (replacing a top nav bar), consistent spacing, and a polished professional look. Use when asked to redesign, modernize, restyle, or "SaaS-ify" a Vue app's navigation or overall layout.
---

# Vue 3 SaaS Sidebar Redesign

Converts a Vue 3 app's top-nav layout into a modern SaaS dashboard layout: fixed left
sidebar navigation, a slim top bar for page-level context, consistent spacing, and a
polished visual system — without changing data-fetching logic, routes, or API contracts.

## When to use this

Triggers: "redesign the UI", "make this look like a SaaS app", "move the nav to a
sidebar", "modernize the layout", "polish the design".

Out of scope: changing what data is fetched, changing business logic, adding/removing
routes or features. This is a visual/structural layout change only.

## Step 0 — Respect project rules first

Check the project's root `CLAUDE.md` (and any nested `client/CLAUDE.md`) for a mandatory
subagent rule before touching any `.vue` file. In this repo, **any creation or
significant modification of a `.vue` file must be delegated to the `vue-expert`
subagent** — do the discovery/planning yourself, then hand off the actual edits.

## Step 1 — Discover the current layout

Before writing any code, read:
1. The root layout component (usually `App.vue`) — find the current nav markup
   (logo, nav links, language/profile/utility widgets) and its `<style>` block.
2. The router config (`main.js` or `router/index.js`) — get the full route list and
   labels, including any i18n keys (e.g. `t('nav.inventory')`).
3. Any global design tokens already in use — colors, font sizes, spacing units,
   border-radius, shadows. **Reuse these exactly.** Do not invent a new palette;
   extract the existing one (e.g. slate/gray neutrals + one accent color) and apply
   it consistently in the new layout.
4. Components currently living in the top nav that need a new home (search bars,
   filter bars, language switchers, profile menus, notification bells).

## Step 2 — Plan the new layout structure

Target structure:

```
<div class="shell">
  <aside class="sidebar">          <!-- fixed left column, full height -->
    <div class="sidebar-logo">...</div>
    <nav class="sidebar-nav">
      <router-link> per route, icon + label, vertical stack
    </nav>
    <div class="sidebar-footer">...</div>  <!-- optional: profile/settings -->
  </aside>
  <div class="main-shell">          <!-- remaining column -->
    <header class="topbar">...</header>   <!-- page title, filters, utility widgets -->
    <main class="content">
      <router-view />
    </main>
  </div>
</div>
```

Layout mechanics:
- Use CSS Grid on the shell: `grid-template-columns: <sidebar-width> 1fr;` (typical
  sidebar width: 240–260px). Avoid `position: fixed` + manual margin math when Grid
  will do — it's less error-prone across viewport sizes.
- Sidebar: full viewport height (`100vh`, or `100dvh` if mobile is in scope), own
  scroll if nav list is long, vertical flex stack (logo → nav → footer).
- Nav items: icon + label, generous vertical rhythm (not cramped), rounded active
  state (background tint + accent-colored text, optionally a left accent bar), hover
  state distinct from active state.
- Move any widgets that lived in the old top nav (language switcher, profile menu,
  notifications) into either the sidebar footer or a slim topbar — don't drop
  functionality, just relocate it.
- If a filter bar existed below the old nav, keep it directly under the topbar,
  full width of the content column, sticky if it was sticky before.

## Step 3 — Establish a consistent spacing system

Pick one spacing scale and apply it everywhere in the redesign (4px or 8px base is
typical: 4, 8, 12, 16, 24, 32). Concretely:
- Sidebar padding, nav item padding, topbar padding, and page/card padding should all
  be values from the same scale — no arbitrary one-off `padding: 13px`.
- Card/section gaps (`gap` in flex/grid) should also come from the scale.
- If the codebase already defines spacing via CSS custom properties, use them; if not,
  don't feel obligated to introduce a full token system — just be consistent.

## Step 4 — Delegate implementation to vue-expert

Hand the vue-expert subagent a concrete, self-contained brief (it has no memory of
this conversation), including:
- The exact route list with labels/icons to render in the sidebar.
- The existing color palette and spacing values you extracted in Step 1.
- Which widgets move from the old top nav and where they should land.
- The target grid structure from Step 2.
- Explicit instruction: **do not change any data loading, API calls, or component
  logic — this is a layout/CSS and markup-only change.**
- Instruction to keep `router-link` active-state logic (e.g. `$route.path === '/x'`)
  working, updated for vertical nav styling (`aria-current="page"` on the active link
  for accessibility).
- Instruction to check every view under `client/src/views/*.vue` for any
  layout assumptions tied to the old top-nav height/margins (e.g. hardcoded
  `margin-top`) and adjust so nothing overlaps or leaves dead space.

## Step 5 — Verify

1. Start the app (frontend dev server; backend only if data rendering needs checking).
2. Use Playwright MCP to visit every route and confirm:
   - Sidebar renders full-height with no gaps, active link matches current route.
   - No layout shift/overlap between sidebar, topbar, and content across the routes
     that had different content heights.
   - Relocated widgets (language switcher, profile menu, filters) still function.
   - Check a narrow viewport (e.g. 375px) to confirm the layout doesn't break, even
     if full responsive/collapse behavior isn't in scope — nothing should be totally
     unusable.
3. Check the browser console for errors/warnings introduced by the change.

## Design references (do / avoid)

**Do:**
- Reuse existing brand color(s) and neutrals; only add accent tints (light
  background versions of the accent color) for active/hover states.
- Give the sidebar clear visual separation from content (subtle border or shadow,
  not a hard black line).
- Keep icons consistently sized and aligned with their labels.
- Preserve semantic HTML (`<aside>`, `<nav>`, `<header>`, `<main>`).

**Avoid:**
- Introducing a new color palette unrelated to the existing design system.
- Emojis as icons in a business/professional UI (check root `CLAUDE.md` for an
  explicit no-emoji rule before adding any icon set).
- Collapsing distinct concerns (nav, filters, page content) into one unstructured
  block — keep the sidebar/topbar/content separation clean.
- Silently dropping a feature that lived in the old nav because it "didn't fit" the
  new layout — find it a home instead.
