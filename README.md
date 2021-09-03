# Particles CSS

An atomic CSS-in-JS library with zero runtime.

Features:
- Deduplicates CSS properties to reduce stylesheet size.
- Works with any plain old CSS.
- If you know CSS, there's nothing to learn.
- Supports [pseudo-classes and pseudo-elements](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors/Pseudo-classes_and_pseudo-elements)
- Supports media queries without duplication.
- Define reusable variables, design tokens, or components.
- TypeScript-powered intellisense.

## How it works

Write your CSS properties as a JavaScript style object or as a string. At build time those style definitions get replaced with a string of corresponding classes and a stylesheet is generated.
