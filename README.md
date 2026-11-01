# Design Research — Open-source UI libraries

Research notes on open-source UI component libraries and practical interface design.

**Study notes:** see [STUDY-NOTES.md](STUDY-NOTES.md) for the full comparative study, comparison matrix and reading path.

**Design craft:** see [界面设计技巧](DESIGN-CRAFT.md) for practical guidance on hierarchy, whitespace, typography, color, motion and interaction.

**Site studies:** see [Canvas UI 设计美学](CANVAS-UI-NOTES.md) for an aesthetic teardown of [canvasui.dev](https://canvasui.dev/).

The local `study/` directory contains shallow clones (`--depth 1`) used for source reading and is ignored by Git. Update a local clone with `git -C study/<folder> pull`. Source links in the notes point to the commits used in the study.

| Local folder | Repo | What it is |
|---|---|---|
| `study/shadcn-ui_ui` | [shadcn-ui/ui](https://github.com/shadcn-ui/ui) | Copy-paste components on Radix + Tailwind |
| `study/radix-ui_primitives` | [radix-ui/primitives](https://github.com/radix-ui/primitives) | Unstyled accessible primitives (shadcn's base) |
| `study/mui_base-ui` | [mui/base-ui](https://github.com/mui/base-ui) | Unstyled primitives from Radix/MUI team |
| `study/tailwindlabs_headlessui` | [tailwindlabs/headlessui](https://github.com/tailwindlabs/headlessui) | Unstyled components from Tailwind team |
| `study/chakra-ui_ark` | [chakra-ui/ark](https://github.com/chakra-ui/ark) | Headless components built on Zag.js state machines |
| `study/heroui-inc_heroui` | [heroui-inc/heroui](https://github.com/heroui-inc/heroui) | Styled React + Tailwind library (formerly NextUI) |
| `study/mantinedev_mantine` | [mantinedev/mantine](https://github.com/mantinedev/mantine) | Full-featured React component library |
| `study/chakra-ui_chakra-ui` | [chakra-ui/chakra-ui](https://github.com/chakra-ui/chakra-ui) | Styled, themeable React components |
| `study/adobe_react-spectrum` | [adobe/react-spectrum](https://github.com/adobe/react-spectrum) | React Aria hooks + Spectrum design system |
| `study/saadeghi_daisyui` | [saadeghi/daisyui](https://github.com/saadeghi/daisyui) | Tailwind CSS component classes |
| `study/magicuidesign_magicui` | [magicuidesign/magicui](https://github.com/magicuidesign/magicui) | Animated components, shadcn-style |
| `study/ibelick_motion-primitives` | [ibelick/motion-primitives](https://github.com/ibelick/motion-primitives) | Motion/animation components, shadcn-style |
| `study/origin-space_originui` | [origin-space/originui](https://github.com/origin-space/originui) | Large set of shadcn-compatible components |
| `study/tremorlabs_tremor` | [tremorlabs/tremor](https://github.com/tremorlabs/tremor) | Dashboard and chart components |
| `study/unovue_shadcn-vue` | [unovue/shadcn-vue](https://github.com/unovue/shadcn-vue) | shadcn/ui port for Vue |
| `study/huntabyte_shadcn-svelte` | [huntabyte/shadcn-svelte](https://github.com/huntabyte/shadcn-svelte) | shadcn/ui port for Svelte |
