# Particles CSS

**This project is currently private. If you want to follow the journey, [sign up for my newsletter](https://austingil.com/newsletter). You can also [follow me on Twitter](https://twitter.com/Stegosource) or [star this project on GitHub](https://github.com/AustinGil/prtcls).**

An Atomic CSS-in-JS library with zero runtime overhead and CSS deduplication. Built by [Austin Gil](https://austingil.com).

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

## Benefits

### Plain CSS
The library uses plain old CSS which has a lot of benefits. Developers that already know CSS won't need to learn anything new. If you don't know CSS, you'll learn it, and that will be valuable whether you use this library or not. You can copy and paste CSS to and from any other project. And because it's CSS, you don't have to work within limited rules.

### Design Tokens
Within the configuration file, you can provide design tokens that can be referenced in your CSS. These design tokens allow you to define variables or collections of styles to reuse or extend. For example, maybe you want to maintain a limited set of spacing options to choose from. Or maybe you want to define the default styles for buttons, then extend them for different variations.

### Less Thinking
The library handles generating classes for you, which means you don't have to bother remembering a list of classes. You also don't have to spend time thinking of what to name your classes, or come up with complicated naming conventions. TypeScript support also helps provide autocomplete suggestions for CSS rules or available design tokens you've defined.

### Performance
Runtime JavaScript is one of the biggest deteriorators to performance. This project strips out the runtime JavaScript and replaces it with the static string of atomic CSS classes. Your styles are added to a CSS file that only inlcudes the styles you use, meaning there is no unused CSS in the final bundle, you don't rely on a purge step, and you can avoid flash of unstyled content.

### Atomic Classes
Atomic classes you to reuse the same styles throughout your application without duplicating CSS rules. As a result, your application can grow without increasing your CSS file size. Atomic styles also remove the need for scoped CSS because you can add or remove styles as needed. And it makes it's safe to add or remove styles without worrying about breaking other parts of your application.

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

```html
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

```html
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

### JavaScript Style Object

```js
const classList = css({
  color: 'purple',
  padding: '.5rem',
})
```

### String

```js
const classList = css(`
  color: purple;
  padding: .5rem;
`)
```

### Callback functions

```js
const classList = css((t) => {
  return {
    padding: '10px'
    color: t.colors.primary,
  }
})
```
```js
const classList = css((t) => {
  return `
    padding: 10px;
    color: ${t.colors.primary};
  `
})
```
For more details on the callback function parameters, see the configuration section below.

## Configuration
To take advantage of the design tokens feature, you will need to create a configuration file. In your project root, add a file called `.prtcls.config.js`. It should export an object with a `tokens` property. Anything in this object will be available to the callback function syntax.

Assuming your config file looked something like this:
```js
module.exports = {
  tokens: {
    size: {
      8: '.5rem'
    }
  }
}
```
You could use a callback function like this:
```js
const classList = css((t) => {
  return {
    padding: t.size[8],
  }
})
```
The callback function uses TypeScript to provide intellisense for whatever you put in there.

## Features:
- [x] Framework agnostic.
- [x] Supports [pseudo-classes and pseudo-elements](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors/Pseudo-classes_and_pseudo-elements)
- [x] Supports media queries without duplication.
- [x] Define reusable variables, design tokens, or components.
- [x] Define styles with a [JS Style Object](https://www.w3schools.com/jsref/dom_obj_style.asp), a string of CSS, or a callback function** that returns either.
- [x] TypeScript support for config file.
- [ ] Runtime class generator.
- [ ] Nested selectors.
- [ ] Plugin system.
- [ ] Prefix support.
- [ ] Support for custom class name generators.
- [ ] CSS syntax highlighting plugin.
- [ ] Handling shorthand and longhand properties smartly.

\** Callback functions are used to inject config options, but cannot depend on any runtime variables (yet).