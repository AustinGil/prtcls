# Particles CSS

An Atomic CSS-in-JS library with zero runtime overhead and CSS deduplication.

This is a project by [Austin Gil](https://austingil.com) and is currently private. If you want to follow the journey, [sign up for my newsletter](https://austingil.com/newsletter). You can also [follow me on Twitter](https://twitter.com/Stegosource) or [star this project on GitHub](https://github.com/AustinGil/prtcls).

Before transpiling you pass CSS rules to the `css()` function, which returns a string of classes. The `prtcls/styles.css` file is empty:
```js
// your JavaScript file
import { css } from 'prtcls'
const btnRed = css(`
  padding: 10px;
  background: red;
`)
const btnBlue = css(`
  padding: 10px;
  background: blue;
`)
```
```css
/* prtcls/styles.css */
```

After transpiling, the library's footprint is removed and replaced with just the static string of classes. The rules are injected into `prtcls/styles.css` without any duplication:
```js
// your JavaScript file
const btnRed = 'p_10px bg_red'
const btnBlue = 'p_10px bg_blue'
```
```css
/* prtcls/styles.css */
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
- It works with plain CSS. If you know CSS, you're set. No need to learn some library-specific syntax.
- Because it's CSS, there are no styling limitations. You can, however, create specific design tokens.
- All the runtime dependencies get transpiled away so your app loads faster and doesn't have a flash of unstyled content.
- You don't have to remember a list of classes available, or come up with class naming conventions. 
- Any duplicated CSS style gets removes so you never have the same rules twice. The more your app grows, the more you save.
- It has TypeScript support which provides intellisense to help know when you write something wrong.
- Only includes the CSS you add to your project which means no unused CSS and faster build times.
- With themes, you can define variables and/or collections of styles ("component") to reuse or extend.
- Atomic styles means there is no need for scoping styles. Just add the ones you need without the drama.

## How it works

The library accepts any CSS as a [JavaScript style object](https://www.w3schools.com/jsref/dom_obj_style.asp) or a string. At build time the library gets removed and those styles get turned into a string of corresponding classes based on their media query, pseudo selector, property, and value. 
<!-- These classes are added to a CSS file  -->

<!-- ## Configuration -->
<!-- ## Installation -->

<!-- Install the package from NPM: 
```bash
npm install prtcls
``` -->
## Setup

### Babel

Add the [babel](https://babeljs.io/) plugin to your babel config:
```js
module.exports = {
  plugins: ['prtcls/babel.cjs'],
};
```

Include the generated stylesheet somewhere in your project:
```js main.js
import 'prtcls/styles.css'
```

### Webpack

Install [`babel-loader`](https://webpack.js.org/loaders/babel-loader/)

```bash
npm install --save-dev babel-loader
```

Add the loader to your webpack config:

```js
module.exports = {
  module: {
    rules: [
      {
        test: /\.m?js$/,
        use: {
          loader: 'babel-loader',
        }
      }
    ]
  }
}
```

Add the [babel](https://babeljs.io/) plugin to your babel config:
```js
module.exports = {
  plugins: ['prtcls/babel.cjs'],
};
```

Include the generated stylesheet somewhere in your project:
```js main.js
import 'prtcls/styles.css'
```

### Vue CLI

These steps work for Vue.js projects using version 2 and 3.

Add the [babel](https://babeljs.io/) plugin to your babel config:
```js
module.exports = {
  plugins: ['prtcls/babel.cjs'],
};
```

Include the generated stylesheet somewhere in your project:
```js main.js
import 'prtcls/styles.css'
```

The library is not currently available within Single File Component templates. For the Options API, computed properties work well:

```vue
<template>
  <div :class="classes">
    Example
  </div>
</template>
<script>
import { css } from 'prtcls'

const classes = css('text-align: center')

export default {
  computed: {
    classes: () => classes;
  }
}
</script>
```
Or with the Composition API:

```vue
<template>
  <div :class="classes">
    Example
  </div>
</template>
<script>
import { css } from 'prtcls'

const classes = css('text-align: center')

export default {
  setup() {
    return {
      classes: classes
    }
  }
}
</script>
```

### Create React App


For [Create React App](https://create-react-app.dev/) users, it's a bit more involed as they do not allow you to modify the Babel configuration. You can eject, but it's not recommended. So instead we can use the [`customize-cra`](https://github.com/arackaf/customize-cra) and [`react-app-rewired`](https://github.com/haykerp/react-app-rewired) packages to do so.

Install those dependencies:

```bash
yarn add --dev react-app-rewired customize-cra
```

Modify your npm scripts to use `react-app-rewired`

```diff
{
  "scripts": {
-   "start": "react-scripts start",
-   "build": "react-scripts build",
-   "test": "react-scripts test",
-   "eject": "react-scripts eject"
+   "start": "react-app-rewired start",
+   "build": "react-app-rewired build",
+   "test": "react-app-rewired test",
+   "eject": "react-app-rewired eject"
  },
  "devDependencies": {
+   "customize-cra": "^1.0.0",
+   "react-app-rewired": "^2.1.8"
  }
}
```

Add a `config-overrides.js` file to the root of your project to add the babel plugin:

```js
const {
  override,
  addBabelPlugin,
} = require("customize-cra");

module.exports = override(
  addBabelPlugin('prtcls/babel.cjs')
)
```

In any React component:
```jsx
import { css } from 'prtcls'

const className = css('text-align: center')

export default function() {
  return (
    <div className={className}>
      Example
    </div>
  );
};

```

## Usage

JavaScript Style Object:

```js
const classList = css({
  color: 'purple',
  padding: '.5rem',
})
```

String:

```js
const classList = css(`
  color: purple;
  padding: .5rem;
`)
```

Callback function returning a Style Object or string:
```js
const classList = css(() => {
  return {
    color: 'purple',
    padding: '.5rem',
  }
})
```
```js
const classList = css(() => {
  return `
    color: purple;
    padding: .5rem;
  `
})
```
## Features:
- [x] Framework agnostic.
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