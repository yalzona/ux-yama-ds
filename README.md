# Yama Design System

Yama is the UI design system for Sumo Logic's product (logs, metrics, dashboards, SIEM, Mobot). Source of truth: the Yama-DS Figma file. This README and `tokens.json` were drafted from it. When they disagree with Figma, Figma wins; update these files.

## How to use this system

1. Read `tokens.json`. Use its values exactly. Never invent colors, spacing, radii or shadows.
2. Reference **semantic** tokens (`semantic.*`) in UI. Use raw ramps (`color.*`) only to define a new semantic token.
3. Every semantic color has a `light` and a `dark` value. Design both modes unless told otherwise.
4. Use the Figma components listed below as the vocabulary. Compose from them; do not restyle them.

## Foundations

**Typeface.** Lab Grotesque for all UI text, Lab Grotesque Mono for code. If the font is not available, fall back to `system-ui, sans-serif` and `ui-monospace, monospace`.

**Type scale.** Dense, product-UI scale. Body text is 14px, secondary text 12px.
- Page and panel titles: h1 (24, light), h2 (20, light). Section titles: h3 (16, medium).
- Body: body1 (14/21). Dense or secondary: body2 (12/18). Captions: caption (12/16, secondary color).
- Emphasis uses weight (medium 500, bold 700 for table headers), not color.
- Form labels and helper text are 12px; field values are 14px.

**Color.**
- Primary blue (`primary.main`, Primary-60 `#2063d6`) is the single action color: primary buttons, links, focus, selected state.
- Surfaces are neutral. Light mode backgrounds are white and White-30; dark mode uses the Black ramp (Black-100 page, Black-70 secondary).
- Dark mode elevation is expressed by lighter surfaces (`background.paperElevation1` to `8`), not shadows alone.
- Feedback colors (success, warning, critical, info) are for status only, never decoration. Pair color with an icon or label.
- Accent ramps (magenta, ocean, evergreen) are for categorical data and tags, not UI chrome.
- Insight severity has fixed colors: `severity.critical`, `high`, `medium`, `low`.

**Spacing.** 8px base unit. Use the spacing scale (0, 2, 4, 6, 8, 12, 16, 18, 20, 24, 32, 40, 48, 56, 64). Default gaps: 8 between related controls, 16 between groups, 24 between sections.

**Radius.** Small and restrained. Inputs, indicators and navigation use 4px; interactive surfaces and compact surfaces 6px; cards and anchored overlays 8px; blocking dialogs and pills 12px. Do not use fully round shapes except for pills and avatars.

**Elevation.** Seven levels (2 to 8). Menus and tooltips use low levels; dialogs and drawers use higher. Do not stack shadows on dark surfaces; use the elevated surface colors instead.

**Density.** Controls come in regular (40px) and dense (28px). Data-heavy screens (tables, menus, panels) default to dense. Minimum touch/click target is 24px.

**Icons.** 16px grid, `Icon/<name>` naming, one color token per state (`icon.default`, `icon.active`, and so on). Pop-out icons mark actions that open a new browser tab; follow the pop-out usage guidelines in the Icons page of the Figma file (static in buttons and menus, on hover in lists and table cells, 8px from text, right aligned).

## Components (Figma component sets)

Layout and containers: Paper (Elevation), Dashboard Card, Tiles, Dialog, Drawer, Tabbed Drawer, Popover, Divider, State Overlay.
Navigation: Primary Left Navi, Secondary Left Navi, Global Toolbar, Header, Tabs (horizontal and vertical), Tabbed Menu, Breadcrumbs, Pagination, Stepper, Links.
Actions: Button (variants and sizes), Split Button, Button Group (toggle), Feedback Button, Icon Bar.
Inputs: Text Field, Text Area, Select Field, Autocomplete, Search Bar, Masked Input, Number Field, Checkbox, Radio Buttons, Toggle, Date and Time Picker, Color Picker, Color Scheme Picker, Code Editor.
Data display: Table (row, cell, header, column, footer), Nested List, Menu, Chips, Status Chips, Badge, Tooltip.
Feedback: Toasts, Inline Notification, Loaders (Spinner, Skeleton), AI Watermark.

Specs for the components above are in the next section. Known gaps in Figma: Slider (missing), Badge (needs discussion), Number Field (flagged).

## Component specs

Extracted from the default variant of each Figma component set. Sizes are px. Token names refer to `tokens.json` (`semantic.*`, `radius.*`, `spacing.*`). Where a state is listed but not described, it uses the next token step in the same family (hover lighter or darker, disabled uses the secondary text color).

### Actions

**Button** (`<Button>`). Variants: Standard, Icon Only, Text Button. Styles: Primary, Secondary, Outline, Destructive. Sizes: Small (28 tall) and Regular (36 tall). States: Default, Hovered, Active, Disabled. Horizontal padding 12, radius `radius.interaction` (6), 8 between icon and label. Primary fill is `interaction.bg` with `text.contrast` label. Optional left icon (16) and dropdown caret. Secondary uses `button.secondary*` tokens, destructive uses `button.destructive*`, outline uses `button.outlineBorder`.

**Split Button.** Primary or Secondary, Regular (36) or Small. A main button plus a 26px-wide dropdown segment, 2px apart. Show the pop-out indicator on the main segment when it opens a new tab.

**Link.** States: Default, Hovered, Active, Visited, plus an External variant (with pop-out icon). Color `button.primaryTextDefault`; visited uses `text.linkVisited`.

### Inputs

**Text Field** (`<TextField>`). Underline style: label above in `form.label` color, value below, bottom border `input.borderDefault` (1px, 2px on hover, `input.borderActive` when active, `input.borderError` on error). Layouts: Standard, Label-Left, Icon-Left. States: Default, Hovered, Active, Error, Disabled. Types: Editable, Read-Only. Optional helper text (12px, `form.helperText`). Default width 180; stretch to the container.

**Select Field.** Same underline anatomy as Text Field with a 12px `mini-angle-down` caret. Layouts: Standard, Label-Left, Icon-Left, Label-Less, Border-Less. States: Default, Focus, Error, Disabled, Hover.

**Checkbox.** 16 square (Small variant available), radius `radius.selection` (2), border `interaction.borderDefault`, checked fill `interaction.bgChecked`. Status: Off, On, Intermediate. Optional label and helper text.

**Radio Button.** 16 circle, 2px border (`borderWidth.control`). Group with the Radio Button Layout (horizontal or vertical).

**Toggle.** 28 by 16, pill-shaped track with a 16 knob. Off track `grey.30` (light); on track uses the primary tint. Optional label and helper text.

**Search Bar.** Types: Standalone, Standard, Contained. Underline style, 30 tall, 400 wide by default, leading search icon.

### Display

**Chips.** Variants: Standard, Outlined, Label-Value. Sizes: Medium (20 tall) and Small. Pill radius, padding 2 by 6, 6 gap. Editable chips show a 9px close icon. Use for user-entered tags and filters.

**Status Chip.** Types: Info, Success, Critical, Warning, Neutral, Magenta, Teal. Variants: Filled, Outlined, Minimal. 20 tall, pill radius, padding 2 by 8, 12px leading icon, 12px label, `statusChip.*` tokens. Use for object state.

**Table.** Row height 40 (dense 28). Cells have 16 horizontal padding, 8 gap and a bottom border `border.lowContrast`. Header cells use `table.header` fill, 12px bold label in `text.secondary`, and a 1 by 24 divider between columns. Row states: Default, Hovered (`table.rowHovered`), Selected (`table.rowSelected`). Row variants: Standard, Nested. A leading Object Status column (56 wide) can show an icon. Cell types: Icon + String, Checkbox, Chips. Pagination and footer sit below (`table.footer`). Cell text is 14px (12px dense).

**Tabs.** Horizontal tab is 32 tall with 12 horizontal padding and a 3px active bar in `primary.main`. States: Default, Hovered, Disabled. Optional count and status tag (Beta, Preview, New). Vertical tabs also exist.

**Pagination.** 24 controls (first, previous, next, last, page number, page input with 4px radius).

### Overlays and feedback

**Menu.** Items are 40 tall (28 dense) with padding 8 by 16 and 8 gap, minimum width 120. Item states: Enabled, Hovered, Selected, Disabled. Item variants: Standard, Cascading, Multi-Select. Optional leading icon, keyboard shortcut and divider. A menu can add a section header and a footer (helper text or an action). Container: `background.paperElevation4`, radius `radius.large` (8), Elevation 4. Items that open a new tab show the pop-out indicator.

**Dialog.** 24 padding on title and action areas. Actions are right-aligned, secondary left of primary. Blocking dialogs use `radius.overlayBlocking` (12). Several width sizes exist; typical content widths range from about 400 to 530.

**Drawer.** Small (380), Medium (448), Large (648) wide, Paper surface with Elevation 2.

**Tooltip.** Padding 8, radius 8, fill `tooltip.bg`, Elevation 4. Placement: Top, Right, Bottom. Types: Info and Error. Optional links inside.

**Toast.** Minimum height 48, 312 wide by default, radius 8, Elevation 4. Notification types: Default, Success, Warning, Error, Info (colored by `toast.*`). Zero to two links, optional pop-out icon and close button. Use a toast with a link after creating an object.

**Inline Notification.** Types: Standard, Recommendation, Critical, Warning, Positive. Formats: Single-Line (32 tall) and Multi-Line. A colored left bar (`feedback.*`), `background.paperElevation1` fill, `border.lowContrast` outline, optional dismiss.

## Usage rules

- One primary button per view. Secondary actions use secondary or text buttons; destructive actions use the destructive button.
- Use Status Chips for object state (success, warning, critical, info, neutral, plus magenta and teal for categories), never plain colored text.
- Toasts confirm completed actions and may carry a link; use Inline Notification for persistent, in-context messages.
- Tables: dense by default, header on `table.header`, hover and selected rows use the table row tokens.
- Do not introduce new component variants without adding them to Figma first.

## Voice

Follow the Sumo Logic brand voice guidelines for copy: plain, direct, active voice, sentence case for UI labels, no exclamation marks in product UI.

## Contributing

1. Change Figma first (variables, styles, components).
2. Update `tokens.json` and the relevant section here in the same pull request or edit.
3. Add a line to the changelog below with date, what changed and why.
4. Another designer reviews before merge.

## Not yet captured

`tokens.json` includes core semantic tokens and the most-used component tokens (button, table, menu, tooltip, toast, status chip). The remaining component-level tokens (code editor syntax, date picker, scroll bar, tabbed drawer, and others) live in the Figma `palette` collection and have not been exported yet.

## Changelog

See `CHANGELOG.md`.
