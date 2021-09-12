# Particles CSS

An Atomic CSS-in-JS library with zero runtime overhead and CSS deduplication.

This is a project by [Austin Gil](https://austingil.com) and is currently private. If you want to follow the journey, [sign up for my newsletter](https://austingil.com/newsletter). You can also [follow me on Twitter](https://twitter.com/Stegosource) or [star this project on GitHub](https://github.com/AustinGil/prtcls).

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
- It works with plain old CSS. If you know CSS already, you're set. If not, you'll learn something useful besides library-specific syntax.
- You can use any valid CSS that you want. There are no limitations (unless you want to create some with themes).
- All the runtime dependencies get transpiled away so your app loads faster and doesn't have a flash of unstyled content.
- You spend less time thinking of new class names, and less energy remembering them. 
- Any duplicated CSS style gets removes so you never have the same rules twice. The more your app grows, the more you save.
- It has TypeScript support which provides intellisense to help know when you write something wrong.
- Only includes the CSS you add to your project which means no unused CSS and faster build times.
- With themes, you can define variables and/or collections of styles ("component") to reuse or extend.

## How it works

The library accepts any CSS as a [JavaScript style object](https://www.w3schools.com/jsref/dom_obj_style.asp) or a string. At build time the library gets removed and those styles get turned into a string of corresponding classes based on their media query, pseudo selector, property, and value. 
<!-- These classes are added to a CSS file  -->

<!-- ## Configuration -->
## Installation

Install the package from NPM: 
```bash
npm install prtcls
```

Add the [babel](https://babeljs.io/) plugin to your config:
```js
const prtclsPlugin = require('prtcls/babel-plugin');

module.exports = {
  // ...
  plugins: [
    prtclsPlugin(),
  ],
};
```

Include the generated stylesheet somewhere in your project:
```js main.js
import 'prtcls/prtcls.css'
```

That's it!

## Usage

JavaScript Style Object:

```js
const classList = getAtomicClasses({
  color: 'purple',
  padding: '.5rem',
})
```

String:

```js
const classList = getAtomicClasses(`
  color: purple;
  padding: .5rem;
`)
```

Callback function returning a Style Object or string:
```js
const classList = getAtomicClasses(() => {
  return {
    color: 'purple',
    padding: '.5rem',
  }
})
```
```js
const classList = getAtomicClasses(() => {
  return `
    color: purple;
    padding: .5rem;
  `
})
```
## Features:
- [x] Famework agnostic.
- [x] Supports [pseudo-classes and pseudo-elements](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors/Pseudo-classes_and_pseudo-elements)
- [x] Supports media queries without duplication.
- [x] Define reusable variables, design tokens, or components.
- [x] Define styles with a [JS Style Object](https://www.w3schools.com/jsref/dom_obj_style.asp), a string of CSS, or a callback function** that returns either.
- [ ] Runtime class generator.
- [ ] Nested selectors.
- [ ] TypeScript support for config file.
- [ ] Plugin system.
- [ ] Prefix support.
- [ ] Support for custom class name generators.
- [ ] Tagged templates literal + CSS syntax highlighting plugin.
- [ ] Handling shorthand and longhand properties smartly.

\** Callback functions are used to inject config options, but cannot depend on any runtime variables (yet).