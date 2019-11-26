<p align="center">
  <img src="./docs/src/images/popper-logo.png" alt="Popper" height="300px"/>
</p>

Positioning tooltips (_but also dropdowns, popovers, and more_) is difficult. **Popper** is here to help!

Given a reference element (such as a button) and a tooltip element, Popper will automatically put your tooltip in the right place next to the button.

### Why Popper?

A naive implementation of a popper element generally doesn't consider the following:

- Preventing overflow when the popper is near a boundary (e.g. `window`), it will get cut off
- Flipping to keep the popper visible in the viewport for the user
- Keeping the popper with the reference element when inside a scrolling container

Popper solves all of these key problems in an elegant, performant manner. It is a ~3 kB library that aims to provide a reliable and extensible positioning engine you can use to ensure all your popper elements are positioned in the right place. Why waste your time writing your own logic every time you are programming a tooltip? There are many edge cases that are easy to forget to consider, which is why we've done the hard work for you.

This library can position any pair of elements in your document without needing to alter the DOM in any way. It doesn't matter if your elements are not close to each other or are in two different scrolling containers, they will always end up in the right position.

Since we write UIs using powerful abstraction libraries such as React or Angular nowadays, you'll also be glad to know Popper can fully integrate with them and be a good citizen together with your other components. Check out [`react-popper`](https://github.com/FezVrasta/react-popper) for the official Popper wrapper for React.

## Installation

### 1. Package Manager

```bash
# With Yarn
yarn add @popperjs/core@next

# With npm
npm i @popperjs/core@next
```

### 2. CDN

```html
<script src="https://unpkg.com/@popperjs/core@next"></script>
```

### 3. Direct Download

Manually downloading the library is not recommended because you lose versioning management that the unpkg CDN or npm/Yarn provide.

You don't receive fix/feat updates easily and will lag behind the website documentation, among other issues, and this quickly becomes an unmaintainable way to manage dependencies.

## Usage

Popper has the ability to work as a plug n' play library with all features included, as well as a tree-shakable library that minimizes bundle size if you import only what you need.

### CDN

Generally, for CDN users, you'll be using the fully-featured `umd` file:

```html
<script src="https://unpkg.com/@popperjs/core@next"></script>
<script>
  // Now the script is loaded, you can use the `Popper` class!
</script>
```

Importing features you need comes at the cost of extra HTTP requests which is usually not worth it.

### Module Bundlers

For users of module bundlers like webpack or Rollup, you're going to want to take advantage of tree-shaking in your bundler. This comes at the cost of extra setup, but is worth it.

In your app, you can do the following:

```js
// Import the core class
import Popper from '@popperjs/core';

// Import the features you need
import {
  computeStyles,
  applyStyles,
  detectOverflow,
  preventOverflow,
} from '@popperjs/core/lib/modifiers';

// Setup Popper's default modifiers for each new instance
Popper.defaultModifiers = [
  detectOverflow,
  preventOverflow,
  computeStyles,
  applyStyles,
];

// Now you can use the `Popper` class with _only_ the features you want. For
// instance, we aren't using the `arrow`, `flip`, or `offset` modifiers, because
// the current component, route, or our entire app does not need them. This lets
// us save on bundle size bytes for our users!
```

If you don't want to bother with tree-shaking and don't need bundle size cost advantages, you can import the fully featured `esm` file:

```js
// All features included!
import Popper from '@popperjs/core/lib/popper';
```

### Instantiation

Creating a popper instance is done by passing the reference element (such as a button), the popper element (such as a tooltip), and some options to the `Popper` constructor:

```js
// Get your elements
const element = document.querySelector('#button');
const popper = document.querySelector('#tooltip');

// Let Popper do the magic!
new Popper(element, popper, { placement: 'right' });
```

## Distribution targets

Popper is distributed in 3 different versions, in 3 different file formats.

The 3 file formats are:

- `umd` (works with `<script>` tags or RequireJS)
- `cjs` (works with `require()` syntax)
- `esm` (works with `import` syntax - **recommended**)

The 3 versions are:

- `popper`: includes all the modifiers (features) in one file (**default for `umd`**)
- `popper-lite`: includes only the minimum amount of modifiers to provide the basic functionality
- `popper-base`: doesn't include any modifier, you must import them separately (**default for `esm` and `cjs`**)

Below you can find the size of each version, minified and compressed with
the [Brotli compression algorithm](https://medium.com/groww-engineering/enable-brotli-compression-in-webpack-with-fallback-to-gzip-397a57cf9fc6):

![](https://badge-size.now.sh/https://unpkg.com/@popperjs/core@next/dist/umd/popper.min.js?compression=brotli&label=popper)
![](https://badge-size.now.sh/https://unpkg.com/@popperjs/core@next/dist/umd/popper-lite.min.js?compression=brotli&label=popper-lite)
![](https://badge-size.now.sh/https://unpkg.com/@popperjs/core@next/dist/umd/popper-minimal.min.js?compression=brotli&label=popper-minimal)

## Hacking the library

If you want to play with the library, implement new features, fix a bug you found, or simply experiment with it, this section is for you!

First of all, make sure to have [Yarn installed](https://yarnpkg.com/lang/en/docs/install).

Install the development dependencies:

```
yarn install
```

And run the development environment:

```
yarn dev
```

Then, simply open one the development server web page:

```
# macOS and Linux
open localhost:5000

# Windows
start localhost:5000
```

From there, you can open any of the examples (`.html` files) to fiddle with them.

Now any change you will made to the source code, will be automatically
compiled, you just need to refresh the page.

If the page is not working properly, try to go in _"Developer Tools > Application > Clear storage"_ and click on "_Clear site data_".  
To run the examples you need a browser with [JavaScript modules via script tag support](https://caniuse.com/#feat=es6-module).
