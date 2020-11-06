# Cyclic Dependency Fixed Version of React Virtualized

### If you need original React Virtualized [Link](https://github.com/bvaughn/react-virtualized)

[<img src="https://cloud.githubusercontent.com/assets/29597/11737732/0ca1e55e-9f91-11e5-97f3-098f2f8ed866.png" alt="React virtualized" data-canonical-src="https://cloud.githubusercontent.com/assets/29597/11737732/0ca1e55e-9f91-11e5-97f3-098f2f8ed866.png" width="330" height="100" />](https://velusgautam.github.io/react-virtualized/)

[![NPM version](https://img.shields.io/npm/v/@velusgautam/react-virtualized.svg?style=flat)](https://www.npmjs.com/package/@velusgautam/react-virtualized)

[![NPM total downloads](https://img.shields.io/npm/dt/@velusgautam/react-virtualized.svg?style=flat)](https://npmcharts.com/compare/@velusgautam/react-virtualized?minimal=true)

React components for efficiently rendering large lists and tabular data.
Check out [the demo](https://velusgautam.github.io/react-virtualized/) for some examples.

## A word about `react-window`

If you're considering adding `react-virtualized` to a project, take a look at [`react-window`](https://github.com/bvaughn/react-window) as a possible lighter-weight alternative. [Learn more about how the two libraries compare here.](https://github.com/bvaughn/react-window#how-is-react-window-different-from-react-virtualized)

## Getting started

Install `react-virtualized` using npm.

```shell
npm install @velusgautam/react-virtualized --save
```

ES6, CommonJS, and UMD builds are available with each distribution.
For example:

```js
// Most of react-virtualized's styles are functional (eg position, size).
// Functional styles are applied directly to DOM elements.
// The Table component ships with a few presentational styles as well.
// They are optional, but if you want them you will need to also import the CSS file.
// This only needs to be done once; probably during your application's bootstrapping process.
import '@velusgautam/react-virtualized/styles.css';

// You can import any component you want as a named export from 'react-virtualized', eg
import {Column, Table} from '@velusgautam/react-virtualized';

// But if you only use a few react-virtualized components,
// And you're concerned about increasing your application's bundle size,
// You can directly import only the components you need, like so:
import AutoSizer from '@velusgautam/react-virtualized/dist/commonjs/AutoSizer';
import List from '@velusgautam/react-virtualized/dist/commonjs/List';
```

Note webpack 4 makes this optimization itself, see the [documentation](https://webpack.js.org/guides/tree-shaking/#mark-the-file-as-side-effect-free).

If the above syntax looks too cumbersome, or you import react-virtualized components from a lot of places, you can also configure a Webpack alias. For example:

```js
// Partial webpack.config.js
{
  alias: {
    'react-virtualized/List': '@velusgautam/react-virtualized/dist/es/List',
  },
  ...rest
}
```

Then you can just import like so:

```js
import List from 'react-virtualized/List';

// Now you can use <List {...props} />
```

You can also use a global-friendly UMD build:

```html
<link rel="stylesheet" href="path-to-react-virtualized/styles.css" />
<script src="path-to-react-virtualized/dist/umd/react-virtualized.js"></script>
```

Now you're ready to start using the components.
You can learn more about which components react-virtualized has to offer [below](#documentation).

## Dependencies

React Virtualized has very few dependencies and most are managed by NPM automatically.
However the following peer dependencies must be specified by your project in order to avoid version conflicts:
[`react`](https://www.npmjs.com/package/react),
[`react-dom`](https://www.npmjs.com/package/react-dom).
NPM will not automatically install these for you but it will show you a warning message with instructions on how to install them.

## Pure Components

By default all react-virtualized components use [`shallowCompare`](https://facebook.github.io/react/docs/shallow-compare.html) to avoid re-rendering unless props or state has changed.
This occasionally confuses users when a collection's data changes (eg `['a','b','c']` => `['d','e','f']`) but props do not (eg `array.length`).

The solution to this is to let react-virtualized know that something external has changed.
This can be done a couple of different ways.

###### Pass-thru props

The `shallowCompare` method will detect changes to any props, even if they aren't declared as `propTypes`.
This means you can also pass through additional properties that affect cell rendering to ensure changes are detected.
For example, if you're using `List` to render a list of items that may be re-sorted after initial render- react-virtualized would not normally detect the sort operation because none of the properties it deals with change.
However you can pass through the additional sort property to trigger a re-render.
For example:

```js
<List {...listProps} sortBy={sortBy} />
```

###### Public methods

`Grid` and `Collection` components can be forcefully re-rendered using [`forceUpdate`](https://facebook.github.io/react/docs/component-api.html#forceupdate).
For `Table` and `List`, you'll need to call [`forceUpdateGrid`](https://github.com/bvaughn/react-virtualized/blob/master/docs/Table.md#forceupdategrid) to ensure that the inner `Grid` is also updated. For `MultiGrid`, you'll need to call [`forceUpdateGrids`](https://github.com/bvaughn/react-virtualized/blob/master/docs/MultiGrid.md#forceupdategrids) to ensure that the inner `Grid`s are updated.

## Documentation

API documentation available [here](docs/README.md).

There are also a couple of how-to guides:

- [Customizing classes and styles](docs/customizingStyles.md)
- [Displaying items in reverse order](docs/reverseList.md)
- [Using AutoSizer](docs/usingAutoSizer.md)
- [Creating an infinite-loading list](docs/creatingAnInfiniteLoadingList.md)
- [Natural sort Table](docs/tableWithNaturalSort.md)
- [Sorting a Table by multiple columns](docs/multiColumnSortTable.md)

## Examples

Examples for each component can be seen in [the documentation](docs/README.md).

Here are some online demos of each component:

- [ArrowKeyStepper](https://bvaughn.github.io/react-virtualized/#/components/ArrowKeyStepper)
- [AutoSizer](https://bvaughn.github.io/react-virtualized/#/components/AutoSizer)
- [CellMeasurer](https://bvaughn.github.io/react-virtualized/#/components/CellMeasurer)
- [Collection](https://bvaughn.github.io/react-virtualized/#/components/Collection)
- [ColumnSizer](https://bvaughn.github.io/react-virtualized/#/components/ColumnSizer)
- [Grid](https://bvaughn.github.io/react-virtualized/#/components/Grid)
- [InfiniteLoader](https://bvaughn.github.io/react-virtualized/#/components/InfiniteLoader)
- [List](https://bvaughn.github.io/react-virtualized/#/components/List)
- [Masonry](https://bvaughn.github.io/react-virtualized/#/components/Masonry)
- [MultiGrid](https://bvaughn.github.io/react-virtualized/#/components/MultiGrid)
- [ScrollSync](https://bvaughn.github.io/react-virtualized/#/components/ScrollSync)
- [Table](https://bvaughn.github.io/react-virtualized/#/components/Table)
- [WindowScroller](https://bvaughn.github.io/react-virtualized/#/components/WindowScroller)

And here are some "recipe" type demos:

- [Table with resizable (drag and drop) columns](https://codesandbox.io/s/j30k46l7xw)
- [Collapsable tree view](https://rawgit.com/bvaughn/react-virtualized/master/playground/tree.html)
- [Full-page grid (spreadsheet)](https://rawgit.com/bvaughn/react-virtualized/master/playground/grid.html)
- [Dynamic cell measuring](https://rawgit.com/bvaughn/react-virtualized/master/playground/chat.html)
- [Cell hover effects](https://rawgit.com/bvaughn/react-virtualized/master/playground/hover.html)

## Supported Browsers

react-virtualized aims to support all evergreen browsers and recent mobile browsers for iOS and Android. IE 9+ is also supported (although IE 9 will require some user-defined, custom CSS since flexbox layout is not supported).

If you find a browser-specific problem, please report it along with a repro case. The easiest way to do this is probably by forking [this Plunker](https://plnkr.co/edit/6syKo8cx3RfoO96hXFT1).

## Friends

Here are some great components built on top of react-virtualized:

- [react-infinite-calendar](https://github.com/clauderic/react-infinite-calendar): Infinite scrolling date-picker with localization, themes, keyboard support, and more
- [react-sortable-hoc](https://github.com/clauderic/react-sortable-hoc): Higher-order components to turn any list into an animated, touch-friendly, sortable list
- [react-sortable-tree](https://github.com/fritz-c/react-sortable-tree): Drag-and-drop sortable representation of hierarchical data
- [react-virtualized-checkbox](https://github.com/emilebres/react-virtualized-checkbox): Checkbox group component with virtualization for large number of options
- [react-virtualized-select](https://github.com/bvaughn/react-virtualized-select): Drop-down menu for React with windowing to support large numbers of options.
- [react-virtualized-tree](https://github.com/diogofcunha/react-virtualized-tree/): A reactive tree component that aims to render large sets of tree structured data in an elegant and performant way
- [react-timeline-9000](https://github.com/BHP-DevHub/react-timeline-9000/): A calendar timeline component that is capable of displaying and interacting with a large number of items

## Contributions

Use [GitHub issues](https://github.com/velusgautam/react-virtualized/issues) for requests.

I actively welcome pull requests; learn how to [contribute](https://github.com/velusgautam/react-virtualized/blob/master/CONTRIBUTING.md).

## Changelog

Changes are tracked in the [changelog](https://github.com/velusgautam/react-virtualized/blob/master/CHANGELOG.md).

## License

_react-virtualized_ is available under the MIT License.
