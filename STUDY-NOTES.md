# Open-Source UI Component Libraries: A Comparative Study

*Snapshot: 28 October 2026 · Source: the 16 repositories cloned under `study/`*

## Contents

1. [Executive summary](#1-executive-summary)
2. [Scope and method](#2-scope-and-method)
3. [Landscape and taxonomy](#3-landscape-and-taxonomy)
4. [Comparison matrix](#4-comparison-matrix)
5. [shadcn/ui in depth](#5-shadcnui-in-depth)
6. [Library profiles](#6-library-profiles)
7. [Cross-cutting design patterns](#7-cross-cutting-design-patterns)
8. [Selection guide](#8-selection-guide)
9. [Suggested study path](#9-suggested-study-path)
10. [Glossary](#10-glossary)

---

## 1. Executive summary

The 16 libraries form three layers: behaviour primitives at the bottom, copy-paste registries in the middle, and styled or CSS-only systems on top. Most of the set now depends on just four behaviour engines: Radix, Base UI, React Aria and Zag.js.

- **shadcn/ui has become a protocol.** Its registry JSON format and CLI also distribute Magic UI, Motion Primitives and coss ui, and its model has been ported to Vue and Svelte. Each component is now written for three behaviour bases (Radix, Base UI, React Aria) and compiled against eight visual styles. New projects default to Base UI.
- **Styled libraries have stopped building their own behaviour.** HeroUI 3 and React Spectrum S2 sit on React Aria Components, Chakra UI 3 sits on Ark UI and Zag.js, and coss ui sits on Base UI. Mantine is the exception, with its own hooks plus Floating UI.
- **The conventions have converged.** Every Tailwind-based project in the set uses Tailwind v4. Tokens are semantic CSS variables, usually in oklch. State reaches CSS through data attributes, and Floating UI handles positioning almost everywhere.
- **Two licenses need checking.** The coss ui repository mixes AGPL 3.0 and MIT, and HeroUI's license file disagrees with its manifests.

---

## 2. Scope and method

This study covers 16 open-source repositories, each a shallow clone of its default branch taken on 28 October 2026. All findings come from reading the source: package manifests, component implementations, theme files and build tooling. Marketing claims and documentation were not used as evidence.

For each codebase we examined six things: how it is distributed, how it is styled, what supplies accessibility and behaviour, how state is managed, how components compose, and how themes and design tokens are defined.

| Local folder | Upstream repository | Last commit in snapshot | License | Size on disk |
| --- | --- | --- | --- | --- |
| `study/shadcn-ui_ui` | [shadcn-ui/ui](https://github.com/shadcn-ui/ui) | 2026-10-27 | MIT | 83 MB |
| `study/radix-ui_primitives` | [radix-ui/primitives](https://github.com/radix-ui/primitives) | 2026-10-14 | MIT | 8 MB |
| `study/mui_base-ui` | [mui/base-ui](https://github.com/mui/base-ui) | 2026-10-27 | MIT | 33 MB |
| `study/tailwindlabs_headlessui` | [tailwindlabs/headlessui](https://github.com/tailwindlabs/headlessui) | 2026-04-13 | MIT | 6 MB |
| `study/chakra-ui_ark` | [chakra-ui/ark](https://github.com/chakra-ui/ark) | 2026-10-20 | MIT | 133 MB |
| `study/heroui-inc_heroui` | [heroui-inc/heroui](https://github.com/heroui-inc/heroui) | 2026-10-26 | Apache 2.0 file, MIT in manifests | 26 MB |
| `study/mantinedev_mantine` | [mantinedev/mantine](https://github.com/mantinedev/mantine) | 2026-10-25 | MIT | 50 MB |
| `study/chakra-ui_chakra-ui` | [chakra-ui/chakra-ui](https://github.com/chakra-ui/chakra-ui) | 2026-10-23 | MIT | 310 MB |
| `study/adobe_react-spectrum` | [adobe/react-spectrum](https://github.com/adobe/react-spectrum) | 2026-10-27 | Apache 2.0 | 328 MB |
| `study/saadeghi_daisyui` | [saadeghi/daisyui](https://github.com/saadeghi/daisyui) | 2026-10-13 | MIT | 26 MB |
| `study/magicuidesign_magicui` | [magicuidesign/magicui](https://github.com/magicuidesign/magicui) | 2026-10-17 | MIT | 28 MB |
| `study/ibelick_motion-primitives` | [ibelick/motion-primitives](https://github.com/ibelick/motion-primitives) | 2026-09-28 | MIT | 4 MB |
| `study/origin-space_originui` | [origin-space/originui](https://github.com/origin-space/originui) | 2026-10-22 | AGPL 3.0 root, MIT apps | 24 MB |
| `study/tremorlabs_tremor` | [tremorlabs/tremor](https://github.com/tremorlabs/tremor) | 2025-10-10 | Apache 2.0 | 4 MB |
| `study/unovue_shadcn-vue` | [unovue/shadcn-vue](https://github.com/unovue/shadcn-vue) | 2026-10-15 | MIT | 117 MB |
| `study/huntabyte_shadcn-svelte` | [huntabyte/shadcn-svelte](https://github.com/huntabyte/shadcn-svelte) | 2026-10-23 | MIT | 53 MB |

> **Before any reuse:** The coss ui repository (formerly Origin UI) has an AGPL 3.0 license at its root, but its `LICENSING.md` places the app folders under MIT. HeroUI's `LICENSE` file says Apache 2.0, while its package manifests declare MIT. Tremor's most recent commit is a year old, and Headless UI's is six months old, so both are less active than the rest of the set.

---

## 3. Landscape and taxonomy

The libraries fall into three layers, and the behaviour layer underneath decides much of how each one works.

- **Behaviour primitives** (Radix, Base UI, React Aria Components, Ark UI, Headless UI) supply state, keyboard handling and focus management, and ship no styles.
- **Copy-paste registries** (shadcn/ui and its ports, coss ui, Magic UI, Motion Primitives, Tremor Raw) put Tailwind-styled source code directly into your project.
- **Styled systems** (HeroUI, Mantine, Chakra UI, React Spectrum S2) and the CSS-only daisyUI are installed as versioned dependencies.

**Most of the set rests on four behaviour engines.** Each row below is one behaviour family; read across to see what is built on it.

```text
 BEHAVIOUR LAYER             COPY-PASTE REGISTRIES                    STYLED SYSTEMS
 ─────────────────────────   ──────────────────────────────────────   ─────────────────────────
 Radix Primitives            ┌───────────┐  Tremor Raw,
                             │           │  legacy Origin UI
 Base UI                     │ shadcn/ui │  coss ui (formerly Origin UI)
                             │  3 bases  │
 React Aria Components       │  8 styles │                            HeroUI, React Spectrum S2
                             └───────────┘
 Ark UI (Zag.js)                                                      Chakra UI

 Reka UI, Bits UI *          shadcn-vue, shadcn-svelte

 No shared engine            Magic UI, Motion Primitives (motion)     Mantine (own hooks),
 (Headless UI has its own)                                            daisyUI (CSS only)

 * External dependencies of the ports; not among the 16 clones.
```

shadcn/ui is the only library that spans three behaviour families. The Vue and Svelte ports depend on engines outside this set.

---

## 4. Comparison matrix

The libraries differ most on two questions: do you install a dependency or copy the source, and which behaviour layer sits underneath? React Aria and React Spectrum come from the same Adobe repository but are listed separately, because they occupy different layers.

| Library | Distribution | Behaviour base | Styling | Variant API | Frameworks | License |
| --- | --- | --- | --- | --- | --- | --- |
| shadcn/ui | Copy-paste registry and CLI | Radix, Base UI or React Aria | Tailwind v4, oklch CSS variables | cva | React | MIT |
| shadcn-vue | Copy-paste registry and CLI | Reka UI | Tailwind v4, oklch CSS variables | cva | Vue, Nuxt | MIT |
| shadcn-svelte | Copy-paste registry and CLI | Bits UI | Tailwind v4, oklch CSS variables | tailwind-variants | Svelte 5 | MIT |
| coss ui (formerly Origin UI) | shadcn-compatible registry | Base UI (legacy Origin: Radix) | Tailwind v4, palette-derived CSS variables | cva | React | AGPL 3.0 root, MIT apps |
| Magic UI | shadcn-compatible registry | motion | Tailwind v4, shadcn tokens, keyframes | Mostly none | React | MIT |
| Motion Primitives | shadcn-compatible registry and own CLI | motion | Tailwind v4, hard-coded zinc palette | None | React | MIT |
| Tremor Raw | Copy-paste source files | Radix, Recharts, React Aria date picker | Tailwind v4, palette classes | tailwind-variants | React | Apache 2.0 |
| Radix Primitives | npm, one package per component | Own: scoped React context | Unstyled; data attributes and CSS variables | None (unstyled) | React | MIT |
| Base UI | npm, single package with subpaths | Own: store classes, Floating UI | Unstyled; data attributes and CSS variables | None (unstyled) | React | MIT |
| Headless UI | npm, one package per framework | Own: state machines, Floating UI | Unstyled; data attributes, `ui-*` Tailwind variants | None (unstyled) | React, Vue | MIT |
| Ark UI | npm, one package per framework | Zag.js state machines | Unstyled; `data-scope` and `data-part` | None (unstyled) | React, Solid, Vue, Svelte | MIT |
| React Aria Components | npm, umbrella package with subpaths | Own: react-aria hooks, react-stately | Unstyled; render props | None (unstyled) | React | Apache 2.0 |
| HeroUI | npm, two packages | React Aria Components | Tailwind v4, CSS-first BEM classes | tailwind-variants | React | Apache 2.0 file, MIT in manifests |
| Mantine | npm, one package per feature | Own hooks, Floating UI | CSS Modules and CSS variables | `varsResolver` and Styles API | React | MIT |
| Chakra UI | npm, single main package | Ark UI, therefore Zag.js | Emotion at runtime, Panda-style recipes | `defineRecipe` | React | MIT |
| React Spectrum S2 | npm | React Aria Components | Build-time `style()` macro, Spectrum tokens | Conditions inside `style()` | React | Apache 2.0 |
| daisyUI | npm Tailwind plugin | None: CSS only | Tailwind v4 plugin, oklch themes | Modifier classes | Any | MIT |

---

## 5. shadcn/ui in depth

shadcn/ui is no longer a single component set: it is a registry protocol, a CLI and a style compiler. In the snapshot (CLI `shadcn` 4.23.0), each component is written once for each behaviour base (Radix, Base UI or React Aria) and combined with one of eight visual styles at build time.

**Repository layout** (pnpm workspaces, Turbo, Changesets):

| Path | Role |
| --- | --- |
| `apps/v4` | Next.js docs site; also holds the registry source |
| `packages/shadcn` | The CLI |
| `packages/registry` | Fetching, resolving and installing items; schema and transformers |
| `packages/react` | Unstyled React helpers (message-scroller, questionnaire, use-render) |
| `packages/tests` | CLI integration tests (Vitest) |
| `templates/` | Starters for Next.js, Vite, Astro, React Router and TanStack Start |

### 5.1 How a component reaches a project

1. **Authoring.** `apps/v4/registry/bases/{radix,base,aria}/` holds three parallel source trees, each with `ui/`, `lib/`, `hooks/` and `blocks/`. Components use placeholder classes such as `cn-button-variant-default` instead of real Tailwind classes.
2. **Styling.** Eight files, `registry/styles/style-{vega,nova,maia,lyra,mira,luma,sera,rhea}.css`, each about 1,800 lines, define with `@apply` what every placeholder expands to.
3. **Build.** `scripts/build-registry.mts` combines each base with each style, for example `radix-nova` or `base-sera`. `createStyleMap()` (`packages/shadcn/src/styles/create-style-map.ts`) turns the `@apply` rules into a placeholder-to-class map. `transformStyleMap()` then rewrites the placeholders inside `cva()` calls and `className` attributes.
4. **Publish.** `shadcn build` writes one JSON registry item per component, served from `https://ui.shadcn.com/r`.
5. **Install.** `npx shadcn add button` resolves the item and its registry dependencies, installs npm packages, merges CSS variables and writes the files through a transformer chain (5.3).

A legacy `new-york-v4` tree is still authored directly with real class names.

### 5.2 The registry item schema

Defined with zod in `packages/registry/src/registry/schema.ts`. A registry has `name`, `homepage`, `items` and `include`. Each item has:

| Field | Purpose |
| --- | --- |
| `type` | One of `registry:ui`, `block`, `component`, `lib`, `hook`, `page`, `file`, `theme`, `style`, `item`, `base` or `font` |
| `files` | Each file's path, content, type and optional install target |
| `dependencies`, `devDependencies` | npm packages to install |
| `registryDependencies` | Other registry items, given as a bare name, `@namespace/name` or a URL |
| `cssVars` | Theme, light and dark variables merged into the project's CSS |
| `css` | Raw CSS rules, such as `@keyframes` |
| `envVars` | Environment variables to add to the project |
| `tailwind.config` | Legacy configuration for Tailwind v3 projects |

Because any host can serve this JSON, third parties publish their own registries. Magic UI (`@magicui`), coss ui (`@coss`) and Motion Primitives all install through the same CLI, and a project lists these namespaces under `registries` in `components.json`.

### 5.3 components.json and the transformer chain

`components.json` records the project's choices: `style`, `rsc`, `tsx`, `tailwind` (css path, base colour, CSS variables, prefix), `iconLibrary`, `rtl`, `menuColor`, `menuAccent`, `aliases` (components, utils, ui, lib, hooks) and `registries`. `shadcn init` (`packages/shadcn/src/commands/init.ts`) writes it from a preset that bundles style, base colour, icon library, font and radius. New projects default to the Base UI base; existing projects stay on Radix.

On `add`, `packages/registry/src/updaters/update-files.ts` passes every file through these transformers:

- `transformImport` rewrites `@/registry/...` imports to the project's aliases.
- `transformRsc` removes `"use client"` when `rsc` is false.
- `transformCssVars` inlines colours when `cssVariables` is false.
- `transformTwPrefixes` applies a Tailwind class prefix.
- `transformIcons` replaces each `<IconPlaceholder>` with the chosen icon library.
- `transformMenu` applies the configured menu colour.
- `transformAsChild` converts `asChild` into Base UI's `render` prop, for `base-*` styles only.
- `transformRtl`, `transformFont` and `transformCleanup` run last, plus `transformJsx` when `tsx` is false.

CLI commands in this version: `init`, `apply`, `add`, `diff`, `docs`, `view`, `search`, `migrate`, `eject`, `info`, `build`, `mcp`, `preset` and `registry {add, build, validate, mcp}`.

### 5.4 Anatomy of a component

The Radix Button (`apps/v4/registry/bases/radix/ui/button.tsx`) shows the house conventions:

- Variants are declared with `cva`, and their values are placeholders such as `cn-button-size-sm`.
- `asChild` swaps the rendered element for Radix `Slot.Root`.
- The element carries `data-slot="button"`, `data-variant` and `data-size` as styling hooks.
- Class names are merged with `cn`, which now comes from the standalone `cn` package instead of clsx plus tailwind-merge. `npx shadcn migrate cn` converts older projects.
- Compound components are plain function exports (`DialogContent`, `DialogOverlay`), each setting its own `data-slot`.

### 5.5 Theming

- Tokens are oklch CSS variables (`--background`, `--primary`, `--sidebar-*`, `--chart-1` to `--chart-5`) that `@theme inline` maps into Tailwind.
- `--radius` is 0.625rem, and the other radii are multiples of it, for example `--radius-sm: calc(var(--radius) * 0.6)`.
- Seven base colours ship: neutral, zinc, stone, mauve, olive, mist and taupe.
- Dark mode uses a `.dark` class with `@custom-variant dark (&:is(.dark *))` and `next-themes`.
- The shared `shadcn/tailwind.css` defines `data-open`, `data-closed` and `data-checked` variants that match both Radix's `data-state` and Base UI's `data-open`, so one stylesheet serves every base.
- Animation comes from `tw-animate-css`.

---

## 6. Library profiles

Each profile gives the version in the snapshot, the architectural choices that set the library apart, and the files to open first. Paths are relative to each repository folder.

### 6.1 Headless primitives

#### Radix Primitives — `radix-ui` 1.8.1, React only

Radix publishes one npm package per component, 59 for React, and the `radix-ui` umbrella package re-exports all of them. State lives in scoped React contexts (`createContextScope`) and a shared `useControllableState` helper. The `asChild` prop makes a component render `Slot` instead of its own element. `Slot` chains event handlers, joins class names and composes refs. Overlays combine `FocusScope`, `DismissableLayer` and Floating UI positioning, and expose sizes as CSS variables such as `--radix-popover-content-available-height`.

- Tooling: pnpm, Changesets, Vitest (jsdom and RSC projects), `vitest-axe`, Playwright end-to-end tests with axe.
- Read first: `packages/react/slot/src/slot.tsx`, `packages/react/primitive/src/primitive.tsx`, `packages/react/popper/src/popper.tsx`, `packages/react/dismissable-layer/src/dismissable-layer.tsx`, `packages/react/focus-scope/src/focus-scope.tsx`

#### Base UI — `@base-ui/react` 1.9.0, React only

Base UI comes from the MUI team and ships as a single package with one subpath export per component. Composition uses a `render` prop that takes either an element or a function of state; the public `useRender` hook exposes the same mechanism. Popup components keep their state in store classes built on `useSyncExternalStore`. Focus management, dismissal, list navigation and typeahead are all written in this repository; only positioning comes from Floating UI. State is mapped to data attributes automatically, including `data-starting-style` and `data-ending-style` for CSS transitions.

- Tooling: pnpm, Lerna, Nx; Vitest in jsdom or real browsers; Playwright, Argos visual tests and Guidepup screen-reader tests.
- Read first: `packages/react/src/internals/useRenderElement.tsx`, `packages/utils/src/store/ReactStore.ts`, `packages/react/src/internals/getStateAttributesProps.ts`, `packages/react/src/utils/popups/focus/FloatingFocusManager.tsx`, `packages/react/src/utils/popups/interactions/useDismiss.ts`

#### Headless UI — `@headlessui/react` 2.2.10, `@headlessui/vue` 1.7.22

Tailwind Labs publishes one package per framework, and the Vue package has fewer components than the React one. Composition uses the `as` prop (including `as={Fragment}`), render-prop children and class names given as functions. Menu, Listbox and Combobox run on small state-machine classes read through `useSyncExternalStoreWithSelector`. The library depends on Floating UI and borrows `useFocusRing` and `useHover` from React Aria. State is exposed as attributes such as `data-open` and `data-focus`, and `@headlessui/tailwindcss` adds `ui-open:` style variants.

- Tooling: npm workspaces, esbuild, Jest with SWC, Testing Library.
- Read first: `packages/@headlessui-react/src/utils/render.ts`, `packages/@headlessui-react/src/machine.ts`, `packages/@headlessui-react/src/components/menu/menu-machine.ts`, `packages/@headlessui-react/src/internal/floating.tsx`

#### Ark UI — 5.39.3 for React, Solid and Vue; 5.24.3 for Svelte

Ark wraps Zag.js state machines: the React package depends on 68 `@zag-js/*` packages pinned at 1.46.0. Each component calls `useMachine` and then `connect`, which returns prop getters such as `getContentProps()`. Because the behaviour lives in framework-agnostic machines, the same components ship for four frameworks. `asChild` is adapted to each framework: `cloneElement` in React, a function in Solid, a snippet in Svelte 5. Styling hooks are the `data-scope` and `data-part` attributes from Zag's anatomy.

- Note: the Zag source is not in the clone, so its focus-trap, dismissal and positioning behaviour was confirmed from manifests and the lockfile.
- Tooling: Bun workspaces, Changesets, Biome, Vitest, `vitest-axe`, Storybook.
- Read first: `packages/react/src/components/factory.ts`, `packages/react/src/components/popover/use-popover.ts`, `packages/svelte/src/lib/components/factory/factory.svelte`, `packages/solid/src/components/factory.tsx`

### 6.2 Styled component libraries

#### HeroUI — 3.2.6, formerly NextUI

Version 3 is built on React Aria Components; 88 component files import `react-aria-components`. It ships two packages, `@heroui/react` and `@heroui/styles`. Styling is CSS-first Tailwind v4: BEM-style classes such as `.button--primary` are written with `@apply`, and `tailwind-variants` maps props onto them. Tokens are oklch CSS variables mapped into Tailwind through `@theme inline`. Compound components are built with `Object.assign(CardRoot, {Header, Title, ...})`. The `LICENSE` file says Apache 2.0, but the package manifests declare MIT.

- Tooling: pnpm, Turbo, Rollup; Vitest in jsdom and Playwright browser mode.
- Read first: `packages/styles/index.css`, `packages/styles/themes/default/variables.css`, `packages/styles/src/components/button/button.styles.ts`, `packages/react/src/components/button/button.tsx`

#### Mantine — 9.7.4

Mantine has the widest scope in the set: about 120 components in `@mantine/core`, 81 hooks, and separate packages for forms, dates, charts (Recharts), carousel, rich text, notifications, modals and spotlight search. Styling uses CSS Modules and CSS variables. A `varsResolver` in each component turns props into inline CSS variables, so no runtime CSS-in-JS is needed. The theme is a JavaScript object that is converted into `--mantine-*` variables. Behaviour comes from Mantine's own hooks plus Floating UI. The "Styles API" lets consumers target named inner parts through `classNames`, `styles` and `vars`, and `Component.extend()` sets theme-level defaults.

- Tooling: Yarn 4 workspaces, custom build scripts with Rollup, Jest, oxlint and stylelint.
- Read first: `packages/@mantine/core/src/core/MantineProvider/default-theme.ts`, `packages/@mantine/core/src/components/Button/Button.tsx`, `packages/@mantine/core/src/core/factory/factory.tsx`, `packages/@mantine/core/src/core/Box/Box.tsx`

#### Chakra UI — 3.37.0

Version 3 rebuilt Chakra on Ark UI, and therefore on Zag; 133 files import `@ark-ui/react`. Styling uses Panda-style recipes (`defineRecipe`, `defineSlotRecipe`, `createSystem`) that an Emotion-based factory applies at runtime. The `@chakra-ui/panda-preset` package serves teams that want zero-runtime Panda CSS instead. Tokens and semantic tokens, with `_light` and `_dark` values, compile to `--chakra-*` CSS variables. A CLI generates types and copies ready-made snippet compositions into a project.

- Tooling: pnpm, Changesets, Rollup, Vitest, Storybook.
- Read first: `packages/react/src/preset.ts`, `packages/react/src/styled-system/system.ts`, `packages/react/src/styled-system/factory.tsx`, `packages/react/src/theme/recipes/button.ts`, `packages/react/src/components/dialog/dialog.tsx`

#### React Spectrum — `react-aria` 3.53.1, `react-aria-components` 1.22.1, `@react-spectrum/s2` 1.8.2

Adobe's repository is a layered stack:

1. `@internationalized/*` and `react-stately` hold locale data and state.
2. `react-aria` hooks add behaviour and accessibility.
3. React Aria Components package those hooks as unstyled components.
4. The Spectrum design systems are built on top: v3 on Spectrum CSS, S2 on React Aria Components.

The S2 design system styles components with a build-time `style()` macro that emits atomic CSS from Spectrum tokens. It has the strongest internationalisation in the set, with 34 locale files for each component that contains strings. Most `@react-aria/*` and `@react-spectrum/*` packages are now one-line re-exports of the umbrella packages.

- Tooling: Yarn 4, Lerna, Parcel; Jest (including SSR), Vitest browser mode, Chromatic visual tests.
- Read first: `AGENTS.md`, `packages/react-aria-components/src/utils.tsx`, `packages/react-aria-components/src/Button.tsx`, `packages/@react-spectrum/s2/style/style-macro.ts`, `packages/@react-spectrum/s2/src/Button.tsx`

### 6.3 CSS, motion and dashboard collections

#### daisyUI — 5.7.50

daisyUI is a Tailwind v4 plugin of component classes such as `btn` and `btn-primary`, with no runtime JavaScript. Components are plain nested CSS using `@apply`, compiled to JavaScript objects at build time. Variants set local custom properties such as `--btn-color`, and hover and border shades are derived with `color-mix()`. It ships 35 themes defined as oklch semantic tokens and switched with `data-theme`; custom themes use `@plugin "daisyui/theme"`.

- Tooling: Bun workspaces; SvelteKit docs site.
- Read first: `packages/daisyui/index.js`, `packages/daisyui/functions/pluginOptionsHandler.js`, `packages/daisyui/src/components/button.css`, `packages/daisyui/src/themes/light.css`

#### Magic UI

Magic UI is a shadcn-compatible registry of animated components: 78 UI items in `apps/www/registry.json`, installed with `npx shadcn@latest add @magicui/<name>`. 33 of its 79 component files use `motion/react`. The rest use CSS keyframes, which ship with each registry item through its `cssVars` and `css` fields. It reuses shadcn's oklch tokens. A separate `registry.json` at the repository root lists 210 items and appears to be out of date.

- Read first: `apps/www/registry/registry-ui.ts`, `apps/www/scripts/build-registry.mts`, `apps/www/registry/magicui/marquee.tsx`, `apps/www/registry/magicui/blur-fade.tsx`

#### Motion Primitives

A single Next.js app publishes a shadcn-compatible registry of 33 components, all built on `motion/react`. It also has its own CLI (`npx motion-primitives add`). Components hard-code the zinc palette instead of using design tokens. The README describes the project as beta.

- Read first: `components/core/text-effect.tsx`, `components/core/magnetic.tsx`, `scripts/registry-components.ts`, `scripts/registry-build.ts`

#### Tremor Raw

Tremor is a copy-paste collection of 39 dashboard components, each with a version in its file header and its own changelog. Charts wrap Recharts 2.15, inputs and overlays use 18 Radix primitives, and variants use `tailwind-variants`. There are no semantic tokens: colours are hard-coded Tailwind palette classes, and chart colours are mapped in `chartColors.ts`. The latest commit in the snapshot is from October 2025. The older `@tremor/react` npm package is not in this repository.

- Read first: `src/components/AreaChart/AreaChart.tsx`, `src/utils/chartColors.ts`, `src/components/Button/Button.tsx`, `scripts/component-folder.js`

### 6.4 Framework ports and other shadcn-style registries

#### shadcn-vue — 2.8.2

The Vue port mirrors the shadcn CLI command for command and uses the same `@shadcn` namespace pattern. Behaviour comes from Reka UI 2.10, whose `Primitive` component, with its `as` and `as-child` props, takes the place of Radix `Slot`. It ships the same eight style files under a single `reka` base; the sampled files differ from upstream only in quoting. `components.json` uses `typescript` instead of `tsx` and adds `aliases.composables`. When TypeScript is off, `@unovue/detypes` converts single-file components to JavaScript. The `shadcn-nuxt` module auto-registers components with a `Ui` prefix.

- Read first: `apps/v4/registry/bases/reka/ui/button/Button.vue`, `apps/v4/registry/bases/reka/ui/dialog/DialogContent.vue`, `packages/cli/src/utils/transformers/index.ts`, `packages/module/src/module.ts`

#### shadcn-svelte — CLI 1.7.1

The Svelte 5 port is built on Bits UI 2.20. `scripts/pull-styles.ts` copies the style files verbatim from shadcn/ui, they are marked "DO NOT EDIT", and a `parity` package checks class strings against upstream. It uses `tailwind-variants` instead of `cva`. Bits UI's `child` snippet takes the place of `asChild`, and components use runes (`$props()`, `$bindable`).

- Read first: `docs/src/lib/registry/ui/button/button.svelte`, `docs/src/lib/registry/ui/dialog/dialog-content.svelte`, `docs/scripts/build-registry.ts`, `packages/parity/README.md`

#### coss ui, formerly Origin UI

This repository is now the coss.com/ui monorepo, which its README describes as the Cal.com design system; the original Origin UI remains in `apps/origin`. coss ui is built on Base UI 1.9 (`useRender`, `mergeProps`) and published as a shadcn-compatible registry under the `@coss` namespace, which shadcn's own registry directory lists. Legacy Origin UI uses Radix, plus React Aria Components for its date fields. Tokens are built from Tailwind palette references and `color-mix()` rather than oklch literals, and add `info`, `success` and `warning` colours. Licensing is mixed: the root `LICENSE` is AGPL 3.0, but `LICENSING.md` places `apps/origin` and `apps/ui` under MIT.

- Read first: `apps/ui/registry/default/ui/button.tsx`, `apps/ui/registry/default/ui/dialog.tsx`, `packages/ui/src/styles/globals.css`, `apps/ui/AGENTS.md`

---

## 7. Cross-cutting design patterns

Four design problems recur in every codebase: who owns the rendered element, how state reaches CSS, where behaviour comes from, and how tokens are defined. The libraries have converged on a small set of answers to each.

### 7.1 Composition: who owns the rendered element

There are two approaches. *Element merging* (`asChild`) passes props onto a single child element. *Render props* accept a function of state, which also hands the consumer the current state.

| Library | Mechanism | Where to read it |
| --- | --- | --- |
| Radix Primitives | `asChild` makes the component render `Slot`, which chains handlers, joins classes and composes refs | `packages/react/slot/src/slot.tsx` |
| Ark UI | `asChild`, adapted per framework: a cloned element, a function or a Svelte snippet | `packages/react/src/components/factory.ts` |
| Chakra UI | Both `as` and `asChild` on every `chakra.*` element | `packages/react/src/styled-system/factory.tsx` |
| Base UI | `render` prop that takes an element or a function of `(props, state)` | `packages/react/src/internals/useRenderElement.tsx` |
| coss ui | Base UI's `render` prop through `useRender` and `mergeProps` | `apps/ui/registry/default/ui/button.tsx` |
| Headless UI | `as` prop, render-prop children, class names as functions | `packages/@headlessui-react/src/utils/render.ts` |
| React Aria Components | `className`, `style` and `children` as functions of state; slots through contexts | `packages/react-aria-components/src/utils.tsx` |
| Mantine | Polymorphic `component` prop and `renderRoot` | `packages/@mantine/core/src/core/Box/Box.tsx` |
| shadcn-vue, shadcn-svelte | Reka `Primitive` with `as-child`; the Bits UI `child` snippet | per-component files in each registry |

shadcn/ui works with both approaches. Its CLI converts `asChild` into `render` when a project uses the Base UI base.

### 7.2 Exposing state to CSS

Every headless library exposes state as data attributes, so styles can respond without JavaScript. Positioned overlays also publish their measurements as CSS variables.

| Library | State attributes | Positioning variables |
| --- | --- | --- |
| Radix Primitives | `data-state`, `data-side`, `data-align`, `data-highlighted`, `data-disabled`, `data-orientation` | `--radix-popper-available-height`, `--radix-popover-trigger-width` and other per-component aliases |
| Base UI | Generated from every state key, plus `data-starting-style` and `data-ending-style` for transitions | `--available-height`, `--anchor-width`, `--transform-origin` |
| Headless UI | `data-open`, `data-focus` and others, plus `data-headlessui-state` | `--button-width`, `--input-width`, `--anchor-gap` |
| Ark UI (Zag.js) | `data-scope`, `data-part`, `data-state` | `--reference-width`, `--available-height`, `--z-index` |

The styled layers build on these hooks. shadcn/ui's `data-open` variant matches both Radix and Base UI, and Headless UI ships a Tailwind plugin with `ui-open:` variants.

### 7.3 Behaviour and accessibility

- **Positioning is shared.** Floating UI positions overlays in Radix, Base UI, Headless UI, Mantine and Zag.js, the engine behind Ark and Chakra.
- **Focus and dismissal are written in-house.** Radix (`FocusScope`, `DismissableLayer`), Base UI (`FloatingFocusManager`, `useDismiss`) and Headless UI (`FocusTrap` and its hooks) each implement their own focus traps and outside-click handling. React Aria supplies these as hooks, and Headless UI borrows two of them.
- **State models span a spectrum.** At the simple end are context plus a controllable-state hook (Radix, Mantine). Next come external stores read through `useSyncExternalStore` (Base UI, and Headless UI's machine classes). At the formal end are full state machines (Zag.js under Ark and Chakra) and dedicated state hooks (`react-stately` under React Aria and HeroUI).
- **Internationalisation is uneven.** React Aria ships 34 locale files for each component that has strings, plus `@internationalized/date`. Most other libraries leave strings to the consumer.

### 7.4 Theming and design tokens

| Library | Where tokens are defined | Format | Dark mode |
| --- | --- | --- | --- |
| shadcn/ui and its ports | `registry/themes.ts`, mapped with `@theme inline` | oklch CSS variables, radius scale by multiplier | `.dark` class |
| coss ui | `packages/ui/src/styles/globals.css` | Tailwind palette references and `color-mix()` | `.dark` class |
| HeroUI | `packages/styles/themes/default/variables.css` | oklch CSS variables | `.dark` or `data-theme` |
| daisyUI | `packages/daisyui/src/themes/*.css`, 35 themes | oklch semantic tokens | `data-theme`, or the `--prefersdark` flag |
| Mantine | `default-theme.ts`, a JavaScript object | Generated `--mantine-*` variables | `data-mantine-color-scheme` attribute |
| Chakra UI | `src/theme/tokens` and `semantic-tokens` | Generated `--chakra-*` variables | `_light` and `_dark` values on semantic tokens |
| React Spectrum S2 | `@adobe/spectrum-tokens` via `style/tokens.ts` | Atomic CSS using `light-dark()` | `colorScheme` prop on `Provider` |
| Tremor Raw | `src/utils/chartColors.ts` | Hard-coded Tailwind palette classes | `dark:` variants |

Semantic tokens stored as CSS variables are now the norm. Most teams also choose oklch, which keeps perceived lightness steady across hues and makes derived shades predictable.

---

## 8. Selection guide

For a new React and Tailwind project, shadcn/ui is the natural starting point, and its CLI now defaults new projects to the Base UI base. The right choice otherwise follows from three questions: which framework you use, whether you want to own the component source, and how much the library should do for you.

| If the project needs | Start with | Main trade-off |
| --- | --- | --- |
| Owned component source in React with Tailwind | shadcn/ui (Base UI or Radix base) | You maintain the copied code yourself; `shadcn diff` shows upstream changes |
| The same model in Vue or Nuxt | shadcn-vue | Follows upstream with some delay; the Reka UI API differs from Radix in its details |
| The same model in Svelte 5 | shadcn-svelte | Uses Bits UI snippets and tailwind-variants, so React examples do not transfer directly |
| A custom design system on unstyled React primitives | Base UI or Radix Primitives | Base UI is one package with render props; Radix splits into per-component packages and has the larger ecosystem |
| One set of primitives across several frameworks | Ark UI | The behaviour lives in Zag.js, a separate repository you have to read alongside it |
| Strict accessibility and internationalisation | React Aria Components | More concepts to learn: hooks, stately state, collections and render props |
| Styled components on React Aria with Tailwind | HeroUI | Confirm the license: the `LICENSE` file says Apache 2.0, the manifests say MIT |
| A complete toolkit with forms, dates and notifications, without Tailwind | Mantine | A versioned dependency styled with CSS Modules; deep visual changes go through its Styles API |
| A token-driven styled system with style props | Chakra UI | Recipes run on Emotion at runtime; zero-runtime CSS needs the Panda preset |
| Styling only, in any framework or server-rendered HTML | daisyUI | No behaviour: focus management and keyboard handling must come from elsewhere |
| Dashboards and charts | Tremor Raw, or Mantine and Chakra chart packages | Tremor's last commit is from October 2025; all three wrap Recharts |
| Animated marketing and landing pages | Magic UI or Motion Primitives | Adds the `motion` dependency; Motion Primitives hard-codes its palette |
| Base UI components in the shadcn style, at larger scale | coss ui | Check which folder you copy from: the root license is AGPL 3.0, the app folders are MIT |

---

## 9. Suggested study path

Read from the bottom of the stack upward: the primitives first, then shadcn/ui, which is built from them, then the styled systems as a contrast. Local checkouts live under `study/`. Source links point to the exact commits used in this snapshot.

- [ ] **1. The `asChild` pattern.** Read [`study/radix-ui_primitives/packages/react/slot/src/slot.tsx`](https://github.com/radix-ui/primitives/blob/eb3a2b7091293e27df8f9ba906632d8daa3d81a3/packages/react/slot/src/slot.tsx), then [`study/radix-ui_primitives/packages/react/primitive/src/primitive.tsx`](https://github.com/radix-ui/primitives/blob/eb3a2b7091293e27df8f9ba906632d8daa3d81a3/packages/react/primitive/src/primitive.tsx). These two files explain half of the shadcn/ui source.
- [ ] **2. One overlay from start to finish.** Follow [`popover.tsx`](https://github.com/radix-ui/primitives/blob/eb3a2b7091293e27df8f9ba906632d8daa3d81a3/packages/react/popover/src/popover.tsx) into [`popper.tsx`](https://github.com/radix-ui/primitives/blob/eb3a2b7091293e27df8f9ba906632d8daa3d81a3/packages/react/popper/src/popper.tsx), [`dismissable-layer.tsx`](https://github.com/radix-ui/primitives/blob/eb3a2b7091293e27df8f9ba906632d8daa3d81a3/packages/react/dismissable-layer/src/dismissable-layer.tsx) and [`focus-scope.tsx`](https://github.com/radix-ui/primitives/blob/eb3a2b7091293e27df8f9ba906632d8daa3d81a3/packages/react/focus-scope/src/focus-scope.tsx).
- [ ] **3. The render-prop alternative.** Read [`useRenderElement.tsx`](https://github.com/mui/base-ui/blob/cc9075a414c93577a10b3085dbc5f122ea2fe564/packages/react/src/internals/useRenderElement.tsx), [`getStateAttributesProps.ts`](https://github.com/mui/base-ui/blob/cc9075a414c93577a10b3085dbc5f122ea2fe564/packages/react/src/internals/getStateAttributesProps.ts) and [`ReactStore.ts`](https://github.com/mui/base-ui/blob/cc9075a414c93577a10b3085dbc5f122ea2fe564/packages/utils/src/store/ReactStore.ts).
- [ ] **4. Hooks as the foundation.** Read [`study/adobe_react-spectrum/AGENTS.md`](https://github.com/adobe/react-spectrum/blob/0752308bb18ca03e55c06892bf8dbf81760c7f78/AGENTS.md) for the layering, then [`Button.tsx`](https://github.com/adobe/react-spectrum/blob/0752308bb18ca03e55c06892bf8dbf81760c7f78/packages/react-aria-components/src/Button.tsx) and [`utils.tsx`](https://github.com/adobe/react-spectrum/blob/0752308bb18ca03e55c06892bf8dbf81760c7f78/packages/react-aria-components/src/utils.tsx) in React Aria Components.
- [ ] **5. State machines.** Read [`use-popover.ts`](https://github.com/chakra-ui/ark/blob/c7af88a51b9dc32e5903a75b3d49b4deaa36e8dc/packages/react/src/components/popover/use-popover.ts) and [`factory.ts`](https://github.com/chakra-ui/ark/blob/c7af88a51b9dc32e5903a75b3d49b4deaa36e8dc/packages/react/src/components/factory.ts) in Ark UI to see how `useMachine` and `connect` produce prop getters.
- [ ] **6. One shadcn component on three bases.** Compare the [Radix](https://github.com/shadcn-ui/ui/blob/96da9cc7f1aa10580a3741664e2a77c721206c00/apps/v4/registry/bases/radix/ui/button.tsx), [Base UI](https://github.com/shadcn-ui/ui/blob/96da9cc7f1aa10580a3741664e2a77c721206c00/apps/v4/registry/bases/base/ui/button.tsx) and [React Aria](https://github.com/shadcn-ui/ui/blob/96da9cc7f1aa10580a3741664e2a77c721206c00/apps/v4/registry/bases/aria/ui/button.tsx) buttons, then open [`style-nova.css`](https://github.com/shadcn-ui/ui/blob/96da9cc7f1aa10580a3741664e2a77c721206c00/apps/v4/registry/styles/style-nova.css) to see what the `cn-*` placeholders become.
- [ ] **7. The registry pipeline.** Read [`create-style-map.ts`](https://github.com/shadcn-ui/ui/blob/96da9cc7f1aa10580a3741664e2a77c721206c00/packages/shadcn/src/styles/create-style-map.ts), [`schema.ts`](https://github.com/shadcn-ui/ui/blob/96da9cc7f1aa10580a3741664e2a77c721206c00/packages/registry/src/registry/schema.ts), [`update-files.ts`](https://github.com/shadcn-ui/ui/blob/96da9cc7f1aa10580a3741664e2a77c721206c00/packages/registry/src/updaters/update-files.ts) and [`init.ts`](https://github.com/shadcn-ui/ui/blob/96da9cc7f1aa10580a3741664e2a77c721206c00/packages/shadcn/src/commands/init.ts).
- [ ] **8. The ports.** Compare step 6 with the Vue [`Button.vue`](https://github.com/unovue/shadcn-vue/blob/de1f76cbb4b319ea26b0dea175dc00c18fce3bd0/apps/v4/registry/bases/reka/ui/button/Button.vue) and the Svelte [`button.svelte`](https://github.com/huntabyte/shadcn-svelte/blob/6149e14107a9de3530a3083de2f1b7623b3c5d1f/docs/src/lib/registry/ui/button/button.svelte).
- [ ] **9. One button, five styling engines.** Read the button in [Mantine](https://github.com/mantinedev/mantine/blob/1d8c524fac27bc6ede5441cdff79abceb9e95b5c/packages/@mantine/core/src/components/Button/Button.tsx), [Chakra](https://github.com/chakra-ui/chakra-ui/blob/960ae222ace1df8de835dc3c62d698f1b58b6786/packages/react/src/theme/recipes/button.ts), [HeroUI](https://github.com/heroui-inc/heroui/blob/70a11531fedfb39b6a0748ca49766266108362ae/packages/styles/src/components/button/button.styles.ts), [React Spectrum S2](https://github.com/adobe/react-spectrum/blob/0752308bb18ca03e55c06892bf8dbf81760c7f78/packages/@react-spectrum/s2/src/Button.tsx) and [daisyUI](https://github.com/saadeghi/daisyui/blob/bf3bac3a397b543e55641ecb2d60a2ed961f09ec/packages/daisyui/src/components/button.css).
- [ ] **10. Third-party registries.** Finish with Magic UI's [`registry-ui.ts`](https://github.com/magicuidesign/magicui/blob/efe76fc5755eca1142dd4f74c1d6f0ace2887e3c/apps/www/registry/registry-ui.ts) and [`build-registry.mts`](https://github.com/magicuidesign/magicui/blob/efe76fc5755eca1142dd4f74c1d6f0ace2887e3c/apps/www/scripts/build-registry.mts), Motion Primitives' [`registry-build.ts`](https://github.com/ibelick/motion-primitives/blob/120f64f6ca60348e251f929e9c81f11ccbe45eda/scripts/registry-build.ts), and the Base UI button in [coss ui](https://github.com/origin-space/originui/blob/3d8ca28e7d90123e9e0f44665944dc240b026ccb/apps/ui/registry/default/ui/button.tsx).

---

## 10. Glossary

| Term | Meaning in this study |
| --- | --- |
| Headless (unstyled) component | A component that supplies behaviour, state and accessibility but ships no visual styles. The consumer provides all CSS. |
| Primitive | A low-level headless building block, such as Dialog, Popover or Tabs, intended to be wrapped by a design system. |
| Copy-paste registry | A distribution model in which component source code is copied into the consumer's project, usually by a CLI, instead of being installed as a versioned dependency. |
| Registry item | One installable unit in a registry: its files, npm dependencies, other registry dependencies and CSS variables, described as JSON. |
| Compound component | A component split into named parts that share state through context, for example `Dialog.Root`, `Dialog.Trigger`, `Dialog.Content`. |
| asChild / Slot | A Radix pattern in which a component renders its single child element instead of its own, merging props, refs and event handlers onto that child. |
| Render prop | A prop that receives a function or element used to render the component's output, giving the consumer control of the DOM element. |
| Polymorphic component | A component whose rendered element can be changed through a prop such as `as` or `component`. |
| Controlled / uncontrolled state | Controlled state is owned by the parent and passed in through props; uncontrolled state is held internally with an optional default value. |
| State machine | A model in which a component moves between named states through defined transitions. Zag.js uses this approach. |
| Data attributes | Attributes such as `data-state="open"` or `data-disabled` that expose component state to CSS selectors. |
| Design token | A named design value, such as a colour, radius or spacing step, usually exposed as a CSS custom property. |
| Semantic token | A token named by purpose rather than appearance, for example `--primary` or `--destructive` instead of `--blue-600`. |
| Variant API | A typed function that maps props such as `variant` and `size` to class names. Examples: cva (class-variance-authority) and tailwind-variants. |
| Focus trap / focus scope | Logic that keeps keyboard focus inside a region, such as an open modal, until it closes. |
| Roving tabindex | A keyboard pattern in which only one item in a group is tabbable and the arrow keys move focus between items. |
| Dismissable layer | Logic that closes an overlay on Escape or an outside click and manages stacked overlays correctly. |
| WAI-ARIA Authoring Practices | The W3C guidance that defines the expected roles, states and keyboard behaviour for common widgets. |
| oklch | A CSS colour space defined by lightness, chroma and hue, designed so equal lightness values look equally bright across hues. |
