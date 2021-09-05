# Particles CSS

An atomic CSS-in-JS library with zero runtime overhead. Pass in any CSS you want and it spits out a string of atomic/utility CSS classes. At build time, the library is transpiled away and you're left with a static string and a CSS file with only the styles you need.

Before transpiling:
```js
// your JavaScript file
import { prtcls } from 'prtcls'
const classList = prtcls(`
  padding: 10px;
  background: purple;
`)
console.log(classList)
```
```css
/* prtcls.css */
```
After transpiling:
```js
// your JavaScript file
const classList = 'p_10px bg_purple'
console.log(classList)
```
```css
/* prtcls.css */
.p_10px {
  padding: 10px;
}
.bg_purple {
  background: purple;
}
```

Benefits:
- It's really easy to learn. You just need to call a JavaScript function. The rest is CSS.
- You can use any valid CSS that you want. You don't have to work within a limited set (unless you want to).
- It has no JavaScript runtime dependencies. It get's transpiled away.
- Removes any duplicated CSS so you never have the same rules twice.
- It has TypeScript support which provides intellisense to help know when you write something wrong.

Features:
- Supports [pseudo-classes and pseudo-elements](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors/Pseudo-classes_and_pseudo-elements)
- Supports media queries without duplication.
- Define reusable variables, design tokens, or components.
- Define styles with a [JS Style Object](https://www.w3schools.com/jsref/dom_obj_style.asp), a string of CSS, or a callback function** that returns either.

\** Callback functions are used to inject config options, but cannot depend on any runtime variables (yet).

<!-- ## How it works

Write your CSS properties as a JavaScript style object or as a string. At build time those style definitions get replaced with a string of corresponding classes based on the associated media query, pseudo selector, property, and value. These classes are added to a CSS file 
 -->
