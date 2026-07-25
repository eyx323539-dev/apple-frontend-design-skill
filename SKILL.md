---
name: apple-frontend-design
description: Build and refine polished Apple-inspired web interfaces with disciplined typography, spacing, materials, motion, responsive layouts, accessibility, and production-quality frontend implementation. Use when creating dashboards, product pages, settings screens, landing pages, mobile web experiences, or component systems that should feel calm, premium, precise, and recognizably Apple-like without copying proprietary assets.
---

# Apple Frontend Design

Use this skill for the actual interface, not marketing copy about design. Inspect the existing stack and preserve its conventions before introducing new dependencies.

## Design Direction

- Prefer clarity, hierarchy, restraint, and direct manipulation over decoration.
- Make the product or primary task visible in the first viewport.
- Use generous but purposeful whitespace; align content to a consistent grid.
- Keep surfaces mostly unframed. Use cards only for repeated items, dialogs, and genuinely framed tools.
- Never use a large card as the main page container, hero, dashboard canvas, settings page, table shell, or full-width section. Main content must sit directly on the page or within a restrained full-width band.
- Do not simulate page structure with oversized rounded rectangles. Use spacing, dividers, typography, and background changes to establish hierarchy.
- Avoid generic SaaS gradients, glowing blobs, excessive glassmorphism, and nested cards.
- Use real product imagery or meaningful bitmap assets when visuals need to communicate the object or state.
- When presenting a product or feature, use Apple's editorial pattern: a direct product-first headline, concise supporting copy, one clear action, and the next section visible below the fold. Treat copy as part of the interface hierarchy, not filler.
- Use the Codex app as a work-surface reference when building tools: quiet navigation, a persistent task context, readable conversation/content width, restrained toolbar controls, and visible progress/status without visual noise.

## Apple + Codex Reference Pattern

- **Navigation rail:** Keep a calm, light navigation column with clear active state, short labels, familiar line icons, and enough separation between primary actions and recent/history items.
- **Work area:** Give the main task a wide, readable canvas. Use a compact title/toolbar row, then let content occupy the page rather than wrapping everything in cards.
- **Task states:** Show queued, working, waiting for input, success, and error states inline with subtle indicators. Preserve the user's place while status changes.
- **Composer or command area:** Anchor the primary input near the bottom of the work area when the workflow is conversational or command-driven. Keep send/stop/attach actions discoverable and keyboard accessible.
- **Editorial sections:** For marketing or product surfaces, borrow Apple's rhythm: strong title, short paragraph, focused visual, then a clean sequence of full-width sections. Avoid turning each section into a floating panel.
- **Content tone:** Prefer specific, confident, plain-language copy. Keep headings short and literal; put detail in supporting text and progressive disclosure.

Use Apple pages as a content and hierarchy reference, not as a request to copy trademarks, proprietary imagery, exact layouts, or text. Use original assets and product-specific copy.

## Visual System

### Color

- Start with semantic neutrals: background, elevated surface, separator, primary text, secondary text, and accent.
- Prefer near-white/near-black rather than absolute extremes for large surfaces.
- Use one restrained accent color for actions and selection; add semantic red, orange, and green only for status.
- Provide light and dark themes when the app context supports them. Never encode meaning with color alone.

### Typography

- Use the platform system stack: `-apple-system, BlinkMacSystemFont, "SF Pro Display", "SF Pro Text", "Segoe UI", sans-serif`.
- Establish a small type scale with clear roles: display, title, headline, body, footnote, caption.
- Use weight and color to establish hierarchy; do not rely on many font sizes.
- Keep letter-spacing at `0`; avoid cramped all-caps labels.
- Check long labels and localization at narrow widths.

### Shape, Depth, and Materials

- Default to 8px or less radius for compact controls and repeated items; use larger radii only for prominent media or platform-like sheets.
- Use hairline borders and soft, low-alpha shadows. Do not stack multiple dramatic shadows.
- Use translucent material only when it improves hierarchy and preserves contrast; add a solid fallback.
- Keep controls visually stable with explicit min-height, aspect ratio, and padding.

## Interaction and Motion

- Use familiar platform patterns: segmented controls for modes, tabs for peer views, toggles for binary settings, sliders/steppers for numeric values, and menus for option sets.
- Use Lucide or the project's existing icon library. Give unfamiliar icon buttons accessible names and tooltips.
- Make hover, focus, pressed, disabled, loading, empty, error, and success states explicit.
- Animate state changes with short opacity/transform transitions. Use spring-like easing sparingly for sheets, popovers, and reordering.
- Respect `prefers-reduced-motion`; provide a no-motion path.
- Never let animation change layout unexpectedly or obscure content.

## Component and State Contracts

Define these states before implementing any non-trivial screen. Keep dimensions stable so state changes do not move surrounding content.

### Buttons and Controls

- Define default, hover, focus-visible, pressed, disabled, loading, and destructive states.
- Keep a loading button's label context where possible; replace the icon with a spinner only when the action remains unambiguous.
- Disable only when the action cannot be performed. Explain the reason with adjacent text or an accessible description.
- Use a destructive action only when the consequence is clear. Prefer an undo path for reversible changes.

### Dialogs and Confirmation Modals

- Use a dialog for a focused decision, confirmation, or short form; do not put an entire workflow in a dialog.
- Give every dialog a visible title, concise description when needed, explicit primary and secondary actions, and a close button.
- Set initial focus intentionally, trap focus while open, close on `Escape` when safe, and return focus to the trigger after closing.
- Use a destructive confirmation only for irreversible or high-impact actions. State what will happen in plain language and use a specific action label such as `Delete project`, not `Confirm`.
- Prevent accidental dismissal while a form is dirty or a destructive operation is in progress; offer a clear cancel path.
- On mobile, use a bottom sheet or full-screen route when the content needs more room. Keep the primary action reachable above the safe area.
- Implement every create/add action through a modal dialog. The dialog body must be a semantic, structured form with visible field labels, validation, submit progress, error recovery, and explicit cancel and submit actions.
- Keep the page beneath an add dialog focused on browsing or managing existing data. Do not place a permanent add form above, beside, or inside the primary table/list.
- If the add form is too complex for a focused dialog, split it into clear form steps within the dialog or use a full-screen modal on narrow screens; preserve the modal interaction contract.

### Popovers, Menus, and Tooltips

- Use a popover for contextual controls and a menu for a mutually exclusive or command list.
- Anchor overlays to their trigger, keep them within the viewport, and reposition at narrow widths.
- Keyboard users must be able to open, navigate, select, and dismiss menus without a pointer.
- Tooltips are for unfamiliar icon buttons only; never use them as the sole source of essential instructions.
- Do not nest interactive overlays unless the interaction model is explicit and tested.

### Drawers and Sheets

- Use a drawer for secondary context that should remain connected to the current task, such as details, filters, or history.
- Preserve the underlying task context, add an overlay when focus should move to the drawer, and support swipe/close behavior on touch devices.
- Define open, closing, loading, empty, error, and offline states. Keep the drawer width and scroll behavior predictable.

### Loading and Progress

- Use skeletons when the final layout is known and the wait is meaningful; match the approximate shape and density of the real content.
- Use an inline spinner for a short local action and a progress bar for measurable multi-step work.
- Never show a spinner with no context for an indefinite wait. Include a status label or recovery action.
- Preserve already-loaded content during refresh. Use `aria-busy` and a polite live region for meaningful status changes.
- For long-running Codex-like tasks, show queued, running, waiting for approval/input, completed, cancelled, and failed states with timestamps or actionable detail where useful.

### Empty, Error, and Offline States

- Empty states explain what is absent and provide one primary next action. Avoid decorative illustrations that compete with the action.
- Error states say what failed, whether work was saved, and how to recover. Provide retry, edit, or support actions as appropriate.
- Inline validation belongs next to the field; page-level failures belong near the affected task. Preserve user input after errors.
- Offline states distinguish unavailable actions from cached content and provide a retry/sync path.

### Toasts and Notifications

- Use a toast for transient, non-blocking confirmation or warning. Include a concise message and an undo/action link when useful.
- Do not use toasts for required decisions, destructive confirmations, or errors that need user attention.
- Queue or replace repeated toasts rather than covering the interface with duplicates.
- Make toast announcements accessible and ensure they do not block keyboard or touch interaction.

### Forms and Command Areas

- Group related fields with visible labels, helper text, validation, and error text. Do not rely on placeholder text as a label.
- Define pristine, editing, invalid, submitting, saved, and unsaved-exit states.
- Keep the primary submit action stable and show progress without collapsing the form.
- For chat/command composers, support multiline input, submit/stop states, attachment progress, keyboard shortcuts with a visible alternative, and a clear error recovery path.

### Tables, Lists, and Navigation

- Define loading, no-results, empty, selected, hover, keyboard-focus, pagination, and bulk-action states.
- Keep row actions discoverable without requiring hover alone. On mobile, convert secondary columns into a detail view rather than squeezing unreadable columns.
- Preserve navigation context, show the current location, and provide a clear back path for nested workspaces.
- When a table or list supports adding records, place a clear `Add` command in its toolbar. Open a form dialog from that command; refresh or insert the new row after successful submission without losing the user's table state.
- Every data table must provide a global fuzzy search over its declared searchable columns. Debounce input, ignore casing where appropriate, trim whitespace, and clearly distinguish `no matching results` from a genuinely empty dataset.
- Treat structured filters as exact queries. Selects, enums, IDs, statuses, dates, ranges, and boolean filters must map to explicit field predicates rather than fuzzy text matching.
- Support multi-column sorting from sortable headers. Show direction on each active header and a visible priority indicator when more than one sort is active.
- Use a predictable multi-sort gesture or control, such as `Shift` plus click or a dedicated sort menu, and expose an accessible equivalent for keyboard and touch users.
- Cycle sorting through ascending, descending, and unsorted states. Provide a clear way to reset all search, filter, and sort state.
- Preserve fuzzy search, exact filters, multi-sort order, pagination, page size, and selection when opening and closing dialogs or returning from detail views. Store shareable table state in URL parameters when routing supports it.
- For server-side tables, send separate query structures for fuzzy search, exact filters, and ordered sort clauses. Do not concatenate them into an ambiguous free-text query.
- Apply search and filters before pagination. When the query changes, reset to a valid page while preserving page size and sort order.

### Data Access and Query Performance

- Never ship an N+1 query path. Load table rows and their required related data with an appropriate join, eager loading, batching, or a dedicated aggregate query.
- Bound the number of database queries per table request independently of the returned row count. Add an integration test or query-count assertion for relationship-heavy endpoints when the backend test stack supports it.
- Do not query production-sized tables without indexes that match the actual search, exact-filter, join, and sort patterns.
- Index foreign keys used in joins, fields used for exact filters, and columns used for common ordering. Use composite indexes when a frequent query filters and sorts by multiple columns in a stable order.
- Use a suitable full-text, trigram, or search-engine index for fuzzy search on large datasets. Do not apply an unindexed leading-wildcard scan across an unbounded table.
- Verify representative queries with the database's query-plan tool, such as `EXPLAIN` or `EXPLAIN ANALYZE`. Confirm that expected indexes are used and that scanned rows remain proportional to the requested result set.
- Keep pagination bounded and deterministic with a stable tie-breaker. Prefer cursor pagination for large or frequently changing datasets when offset pagination becomes expensive or inconsistent.
- Select only the fields needed by the table and its immediate interactions. Move expensive counts, aggregates, and secondary details into batched or explicitly requested queries.
- Treat missing indexes, full-table scans on user-facing queries, and request-count growth per row as release-blocking defects.

## Layout and Responsive Behavior

- Build from a stable content grid with a readable max width; let primary content breathe before adding side panels.
- Design mobile first for task flow, then enhance for desktop. Do not merely shrink desktop layouts.
- Collapse navigation predictably, keep primary actions reachable, and preserve visible context in sheets/dialogs.
- Use CSS constraints such as `minmax`, `clamp` only for non-font dimensions, `aspect-ratio`, and `container` queries where useful.
- Verify at narrow mobile, normal mobile, tablet, and wide desktop sizes. Text must never overlap, clip, or force accidental horizontal scrolling.

## Accessibility

- Use semantic HTML and correct heading order.
- Make every interactive element keyboard reachable with a visible `:focus-visible` state.
- Keep body text and controls at accessible contrast; test muted text instead of assuming opacity is safe.
- Provide labels, descriptions, error text, and status announcements for form and async states.
- Support reduced motion, zoom, touch targets, and screen-reader names.

## Implementation Workflow

1. Inspect the existing framework, design tokens, routing, icon library, and asset conventions.
2. Define the page hierarchy, key user task, responsive breakpoints, and state matrix before coding.
3. Establish or extend semantic design tokens instead of scattering raw colors and spacing values.
4. Build the primary workflow first, including loading, empty, error, and success states.
5. Add responsive behavior and keyboard/accessibility behavior while implementing, not as a final patch.
6. Review the rendered result at desktop and mobile sizes. Fix hierarchy, spacing, overflow, contrast, and interaction issues before polishing.
7. Run the repository's formatter, type checks, tests, and build. Report anything that could not be run.

## Quality Gate

Before finishing, confirm:

- The first viewport communicates the product and primary action.
- No section is a decorative card inside another decorative card.
- No large card wraps the page, hero, primary workspace, settings body, or data table.
- Every add/create workflow opens a modal whose main content is a semantic form.
- Every data table supports fuzzy search, exact structured filters, and accessible multi-column sorting.
- Table data paths contain no N+1 queries and use verified indexes for search, filters, joins, sorting, and pagination.
- Buttons use icons where a familiar symbol is sufficient and text where the command needs clarity.
- All controls have complete states and accessible names.
- Text fits at mobile and desktop widths without overlap.
- Colors are balanced rather than a single-hue gradient palette.
- Motion is subtle, interruptible, and reduced-motion aware.
- The implementation follows the existing project stack and has no unnecessary dependency or asset churn.
