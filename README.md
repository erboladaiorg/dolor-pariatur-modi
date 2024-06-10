<div align="center">
  <a href="https://npmjs.org/package/@erboladaiorg/dolor-pariatur-modi">
    <img alt="npm" src="https://img.shields.io/npm/v/@erboladaiorg/dolor-pariatur-modi.svg" />
  </a>
  <a href="https://npmjs.org/package/@erboladaiorg/dolor-pariatur-modi">
    <img alt="no dependencies" src="https://badgen.net/bundlephobia/dependency-count/@erboladaiorg/dolor-pariatur-modi" />
  </a>
  <a href="https://npmjs.org/package/@erboladaiorg/dolor-pariatur-modi">
    <img alt="size" src="https://badgen.net/bundlephobia/minzip/@erboladaiorg/dolor-pariatur-modi" />
  </a>
  <a href="https://travis-ci.com/github/AnyRoad/@erboladaiorg/dolor-pariatur-modi">
    <img alt="build" src="https://travis-ci.com/AnyRoad/@erboladaiorg/dolor-pariatur-modi.svg?branch=release" />
  </a>
  <a href="https://codecov.io/gh/anyroad/@erboladaiorg/dolor-pariatur-modi">
    <img alt="coverage" src="https://codecov.io/gh/AnyRoad/@erboladaiorg/dolor-pariatur-modi/branch/release/graph/badge.svg" />
  </a>
  <a href="https://bundlephobia.com/result?p=@erboladaiorg/dolor-pariatur-modi">
    <img alt="tree-shakeable" src="https://badgen.net/bundlephobia/tree-shaking/@erboladaiorg/dolor-pariatur-modi" />
  </a>
  <a href="https://npmjs.org/package/@erboladaiorg/dolor-pariatur-modi">
    <img alt="types included" src="https://badgen.net/npm/types/@erboladaiorg/dolor-pariatur-modi" />
  </a>

  <a href="https://npmjs.org/package/@erboladaiorg/dolor-pariatur-modi">
    <img alt="downloads per month" src="https://img.shields.io/npm/dm/@erboladaiorg/dolor-pariatur-modi" />
  </a>
  
</div>

<div>
  <strong>@erboladaiorg/dolor-pariatur-modi</strong> is a tiny component for React allowing to render JSON as a tree. It focused on the balance between performance for large JSON inputs and functionality. It might not have all the rich features (suce as customization, copy, json editinng) but still provides more than just rendering json with highlighting - e.g. ability to collapse/expand nested objects and override css. It is written in TypeScript and has no dependencies.
</div>

## Install

```bash
npm install --save @erboladaiorg/dolor-pariatur-modi
```

## Migration from the 0.9.x versions

1. Property `shouldInitiallyExpand` has different name `shouldExpandNode` in order to emphasize that it will be called every time properties change.
2. If you use custom styles:
   - `pointer` and `expander` are no longer used
   - component uses `collapseIcon`, `expandIcon`, `collapsedContent` styles in order to customize expand/collapse icon and collpased content placeholder which were previously hardcode to the `▸`, `▾` and `...`.
     Default style values use `::after` pseudo-classes to set the content.

## Usage

```tsx
import * as React from 'react';

import { JsonView, allExpanded, darkStyles, defaultStyles } from '@erboladaiorg/dolor-pariatur-modi';
import '@erboladaiorg/dolor-pariatur-modi/dist/index.css';

const json = {
  a: 1,
  b: 'example'
};

const App = () => {
  return (
    <React.Fragment>
      <JsonView data={json} shouldExpandNode={allExpanded} style={defaultStyles} />
      <JsonView data={json} shouldExpandNode={allExpanded} style={darkStyles} />
    </React.Fragment>
  );
};

export default App;
```

Please note that in JavaScript, an anonymous function like `function() {}` or `() => {}` always creates a different function every time component is rendered, so you might need to use
[useCallback](https://react.dev/reference/react/useCallback) React Hook for the `shouldExpandNode` parameter or extract the function outside the functional component.

### StoryBook

https://anyroad.github.io/@erboladaiorg/dolor-pariatur-modi/

### Props

| Name              | Type                                                     | Default Value | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ----------------- | -------------------------------------------------------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| data              | `Object` \| `Array<any>`                                 |               | Data which should be rendered                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| style             | StyleProps                                               | defaultStyles | Optional. CSS classes for rendering. Library provides two build-in implementations: `darkStyles`, `defaultStyles` (see below)                                                                                                                                                                                                                                                                                                                                 |
| shouldExpandNode  | `(level: number, value: any, field?: string) => boolean` | allExpanded   | Optional. Function which will be called during initial rendering for each Object and Array of the data in order to calculate should if this node be expanded. **Note** that this function will be called again to update the each node state once the property value changed. `level` startes from `0`, `field` does not have a value for the array element. Library provides two build-in implementations: `allExpanded` and `collapseAllNested` (see below) |
| clickToExpandNode | boolean                                                  | false         | Optional. Set to true if you want to expand/collapse nodes by clicking on the node itself.                                                                                                                                                                                                                                                                                                                                                                    |

### Extra exported

| Name              | Type                         | Description                                         |
| ----------------- | ---------------------------- | --------------------------------------------------- |
| defaultStyles     | StyleProps                   | Default styles for light background                 |
| darkStyles        | StyleProps                   | Default styles for dark background                  |
| allExpanded       | `() => boolean`              | Always returns `true`                               |
| collapseAllNested | `(level: number) => boolean` | Returns `true` only for the first level (`level=0`) |

### StyleProps

| Name                    | Type    | Description                                                                                                       |
| ----------------------- | ------- | ----------------------------------------------------------------------------------------------------------------- |
| container               | string  | CSS class name for rendering parent block                                                                         |
| basicChildStyle         | string  | CSS class name for property block containing property name and value                                              |
| collapseIcon            | string  | CSS class name for rendering button collapsing Object and Array nodes. Default content is `▾`.                    |
| expandIcon              | string  | CSS class name for rendering button expanding Object and Array nodes. Default content is `▸`.                     |
| collapsedContent        | string  | CSS class name for rendering placeholder when Object and Array nodes are collapsed. Default contents is `...`.    |
| label                   | string  | CSS class name for rendering property names                                                                       |
| clickableLabel          | string  | CSS class name for rendering clickable property names (requires the `clickToExpandNode` prop to be true)          |
| nullValue               | string  | CSS class name for rendering null values                                                                          |
| undefinedValue          | string  | CSS class name for rendering undefined values                                                                     |
| numberValue             | string  | CSS class name for rendering numeric values                                                                       |
| stringValue             | string  | CSS class name for rendering string values                                                                        |
| booleanValue            | string  | CSS class name for rendering boolean values                                                                       |
| otherValue              | string  | CSS class name for rendering all other values except Object, Arrray, null, undefined, numeric, boolean and string |
| punctuation             | string  | CSS class name for rendering `,`, `[`, `]`, `{`, `}`                                                              |
| noQuotesForStringValues | boolean | whether or not to add double quotes when rendering string values, default value is `false`                        |

## Comparison with other libraries

### Size and dependencies

Here is the size benchmark (using [bundlephobia.com](https://bundlephobia.com)) against similar React libraries (found by https://www.npmjs.com/search?q=react%20json&ranking=popularity):

| Library                  | Bundle size                                                                                                                                  | Bundle size (gzip)                                                                                                                              | Dependencies                                                                                                                                              |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **@erboladaiorg/dolor-pariatur-modi** | [![](https://badgen.net/bundlephobia/min/@erboladaiorg/dolor-pariatur-modi?color=6ead0a&label=)](https://bundlephobia.com/result?p=@erboladaiorg/dolor-pariatur-modi)  | [![](https://badgen.net/bundlephobia/minzip/@erboladaiorg/dolor-pariatur-modi?color=6ead0a&label=)](https://bundlephobia.com/result?p=@erboladaiorg/dolor-pariatur-modi)  | [![](https://badgen.net/bundlephobia/dependency-count/@erboladaiorg/dolor-pariatur-modi?color=6ead0a&label=)](https://bundlephobia.com/result?p=@erboladaiorg/dolor-pariatur-modi)  |
| react-json-pretty        | [![](https://badgen.net/bundlephobia/min/react-json-pretty?color=red&label=)](https://bundlephobia.com/result?p=react-json-pretty)           | [![](https://badgen.net/bundlephobia/minzip/react-json-pretty?color=red&label=)](https://bundlephobia.com/result?p=react-json-pretty)           | [![](https://badgen.net/bundlephobia/dependency-count/react-json-pretty?color=red&label=)](https://bundlephobia.com/result?p=react-json-pretty)           |
| react-json-inspector     | [![](https://badgen.net/bundlephobia/min/react-json-inspector?color=red&label=)](https://bundlephobia.com/result?p=react-json-inspector)     | [![](https://badgen.net/bundlephobia/minzip/react-json-inspector?color=red&label=)](https://bundlephobia.com/result?p=react-json-inspector)     | [![](https://badgen.net/bundlephobia/dependency-count/react-json-inspector?color=red&label=)](https://bundlephobia.com/result?p=react-json-inspector)     |
| react-json-tree          | [![](https://badgen.net/bundlephobia/min/react-json-tree?color=red&label=)](https://bundlephobia.com/result?p=react-json-tree)               | [![](https://badgen.net/bundlephobia/minzip/react-json-tree?color=red&label=)](https://bundlephobia.com/result?p=react-json-tree)               | [![](https://badgen.net/bundlephobia/dependency-count/react-json-tree?color=red&label=)](https://bundlephobia.com/result?p=react-json-tree)               |
| react-json-view          | [![](https://badgen.net/bundlephobia/min/react-json-view?color=red&label=)](https://bundlephobia.com/result?p=react-json-view)               | [![](https://badgen.net/bundlephobia/minzip/react-json-view?color=red&label=)](https://bundlephobia.com/result?p=react-json-view)               | [![](https://badgen.net/bundlephobia/dependency-count/react-json-view?color=red&label=)](https://bundlephobia.com/result?p=react-json-view)               |
| react-json-tree-viewer   | [![](https://badgen.net/bundlephobia/min/react-json-tree-viewer?color=red&label=)](https://bundlephobia.com/result?p=react-json-tree-viewer) | [![](https://badgen.net/bundlephobia/minzip/react-json-tree-viewer?color=red&label=)](https://bundlephobia.com/result?p=react-json-tree-viewer) | [![](https://badgen.net/bundlephobia/dependency-count/react-json-tree-viewer?color=red&label=)](https://bundlephobia.com/result?p=react-json-tree-viewer) |

### Performance

Performance was mesaured using the [react-component-benchmark](https://github.com/paularmstrong/react-component-benchmark) library. Every component was rendered 50 times using the [300Kb json file](https://github.com/erboladaiorg/dolor-pariatur-modi-benchmark/blob/main/src/hugeJson.json) as data source, please refer to source code of the [benchmark project](https://github.com/erboladaiorg/dolor-pariatur-modi-benchmark).
All numbers are in milliseconds. Tests were performed on Macbook Air M1 16Gb RAM usging Chrome v96.0.4664.110(official build, arm64). Every component was tested 2 times but there was no significant differences in the results.

| Library                  | Min   | Max   | Average | Median | P90   |
| ------------------------ | ----- | ----- | ------- | ------ | ----- |
| **@erboladaiorg/dolor-pariatur-modi** | 81    | 604   | 195     | 82     | 582   |
| react-json-pretty        | 22    | 59    | 32      | 24     | 56    |
| react-json-inspector     | 682   | 1 109 | 758     | 711    | 905   |
| react-json-tree          | 565   | 1 217 | 658     | 620    | 741   |
| react-json-view          | 1 403 | 1 722 | 1529    | 1 540  | 1 631 |
| react-json-tree-viewer   | 266   | 663   | 320     | 278    | 455   |

As you can see `react-json-pretty` renders faster than other libraries but it does not have ability to collapse/expand nested objects so it might be good choice if you need just json syntax highlighting.

## License

MIT © [AnyRoad](https://github.com/AnyRoad)
