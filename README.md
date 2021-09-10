# Particles CSS

An atomic CSS-in-JS library with zero runtime overhead and CSS deduplication.

**\*\*This project is currently available to [sponsors](https://github.com/sponsors/AustinGil) until I reach 50 sponsors. After that, I will make the project publicly available.\*\***

Before transpiling:
```js
// your JavaScript file
import { getAtomicClasses } from 'prtcls'
const btnRedClasses = getAtomicClasses(`
  padding: 10px;
  background: red;
`)
const btnBlueClasses = getAtomicClasses(`
  padding: 10px;
  background: blue;
`)
console.log(btnRedClasses, btnBlueClasses)
```
```css
/* prtcls.css */
```
After transpiling:
```js
// your JavaScript file
const btnRedClasses = 'p_10px bg_red'
const btnBlueClasses = 'p_10px bg_blue'
console.log(btnRedClasses, btnBlueClasses)
```
```css
/* prtcls.css */
.p_10px {
  padding: 10px;
}
.bg_red {
  background: red;
}
.bg_blue {
  background: blue;
}
```

#### Benefits:
- If you know CSS, you already know how to use the library. Just pass that into the funciton.
- You can use any valid CSS that you want. You don't have to work within a limited set (unless you want to).
- All the runtime dependencies gets transpiled away which means your app loads faster and no flash of unstyled content.
- Removes any duplicated CSS so you never have the same rules twice. The more your app grows, the more you save.
- It has TypeScript support which provides intellisense to help know when you write something wrong.

## How it works

The library accespt any CSS as a JavaScript style object or a string. At build time the library gets removed and those styles get turned into a string of corresponding classes based on their media query, pseudo selector, property, and value. 
<!-- These classes are added to a CSS file  -->

<!-- ## Configuration -->

## Features:
- [x] Famework agnostic.
- [x] Supports [pseudo-classes and pseudo-elements](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors/Pseudo-classes_and_pseudo-elements)
- [x] Supports media queries without duplication.
- [x] Define reusable variables, design tokens, or components.
- [x] Define styles with a [JS Style Object](https://www.w3schools.com/jsref/dom_obj_style.asp), a string of CSS, or a callback function** that returns either.
- [ ] Runtime class generator.
- [ ] Nested selectors.
- [ ] TypeScript support for config file.

\** Callback functions are used to inject config options, but cannot depend on any runtime variables (yet).
