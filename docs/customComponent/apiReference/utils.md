---
id: utils
title: Utils
---

## Overview

The directory structure for the **utils** folder outlines:

- **utils**:
    - [**common.ts**](#commonts): Contains common utility functions used across the application.
    - [**DataLoader.ts**](#dataloaderts): Defines a DataLoader class for handling data loading operations.
    - [**datasources-helpers.ts**](#datasources-helpersts): Provides helper functions related to data sources.
    - [**date-utils.ts**](#date-utilsts):Includes utility functions for date-related operations.
    - [**Graph.ts**](#graphts): Implements a Graph class for graph-related functionality.
    - **index.ts**: Serves as the entry point for the "utils" module, exporting functions and classes.
    - [**misc.ts**](#miscts): Contains miscellaneous utility functions for various tasks.
    - [**numToMeasurement.ts**](#numtomeasurementts): Converts numerical values to measurement strings.
    - [**PopoverComponents.tsx**](#popovercomponentstsx): Defines React components related to popovers.
    - [**renderComponents.ts**](#rendercomponentsts): Provides a function for rendering components based on a configuration.
    - [**searchComponents.ts**](#searchcomponentsts): Implements a function for searching components based on a search value.
    - [**settingsComponent.tsx**](#settingscomponenttsx): Defines a React component for rendering settings components.
    - [**settingsDefaults.ts**](#settingsdefaultsts): Contains default settings configurations for the application.
    - **subjects.ts**: Defines subjects and actions for communication between different parts of the application using RxJS.
    - [**testUtils.tsx**](#testutilstsx): Contains utility functions for testing, such as creating an editor component for testing scenarios.

<!-- ################################################################################################################
#################################################### common.ts ######################################################
#####################################################################################################################
-->

## common.ts

The `common.ts` file provides utility functions that are commonly used across different parts of the project, promoting code reusability and maintainability.


<!-- ########### reorder ############ -->
### `reorder` Function

#### Purpose
Reorders elements in a list based on the provided start and end indices.

#### Signature
```tsx
reorder<T>(list: T[], startIndex: number, endIndex: number): T[]
```

#### Input

| **Parameter** | **Type** | **Description** |
|---------------|----------|-----------------|
| `list`        | `T[]`    | The array of elements to be reordered. |
| `startIndex`  | `number` | The index of the element to be moved. |
| `endIndex`    | `number` | The index where the element should be placed. |

#### Output

| **Output** | **Description** |
|----------|-----------------|
| `T[]`    | Returns a new array with elements reordered. |

#### Usage Example
```tsx
const originalList = [1, 2, 3, 4, 5];
const reorderedList = reorder(originalList, 2, 4);
// Result: [1, 2, 4, 3, 5]
```

<!-- ########### arrayToTree ############ -->
### `arrayToTree` Function

#### Purpose
Converts a flat array of objects into a tree structure based on specified ID and parent ID keys.

#### Signature
```tsx
arrayToTree = (
  arr: any[],
  options: {
    idKey: string;
    parentKey: string;
    childrenKey: string;
  } = {
    idKey: 'id',
    parentKey: 'parentId',
    childrenKey: 'children',
  },
): any[] => {...};
```

#### Input

| **Parameter** | **Type** | **Description** |
|---------------|----------|-----------------|
| `arr`         | `any[]`  | The flat array to be converted into a tree structure. |
| `options`     | `{}`     | An object containing keys (`idKey`, `parentKey`, `childrenKey`) to customize the conversion. Defaults are provided. |

#### Output

| **Output** | **Description** |
|----------|-----------------|
| `any[]`  | Returns an array representing the tree structure. |

#### Usage Example
```tsx
const flatArray = [
  { id: 1, parentId: null, name: 'Node 1' },
  { id: 2, parentId: 1, name: 'Node 2' },
  { id: 3, parentId: 1, name: 'Node 3' },
];
const treeArray = arrayToTree(flatArray);
// Result: [{ id: 1, parentId: null, name: 'Node 1', children: [{ id: 2, parentId: 1, name: 'Node 2' }, { id: 3, parentId: 1, name: 'Node 3' }] }]
```

<!-- ########### takeOne ############ -->
### `takeOne` Function

#### Purpose
Returns the first element from an iterable or `null` if the iterable is empty.

#### Signature
```tsx
takeOne<T = any>(collection: Iterable<T> | null): T | null
```

#### Input

| **Parameter** | **Type** | **Description** |
|---------------|----------|-----------------|
| `collection`  | `Iterable<T>` \| `null` | The iterable collection from which to take the first element. |

#### Output

| **Output** | **Description** |
|----------|-----------------|
| `T` \| `null`| Returns the first element of the iterable or `null` if the iterable is empty. |

#### Usage Example
```tsx
const exampleArray = [1, 2, 3];
const firstElement = takeOne(exampleArray);
// Result: 1
```

<!-- ########### unsubscribeFromDatasource ############ -->
### `unsubscribeFromDatasource` Function

#### Purpose
Unsubscribes a callback function from a datasource event.

#### Signature
```tsx
unsubscribeFromDatasource = (
  ds: datasources.DataSource,
  cb: () => void,
  eventName: string = 'changed',
): void => {...};
```

#### Input

| **Parameter** | **Type** | **Description** |
|---------------|----------|-----------------|
| `ds`          | `datasources.DataSource` | The datasource from which to unsubscribe the callback. |
| `cb`          | `() => void`             | The callback function to be unsubscribed. |
| `eventName`   | `string`                 | The name of the event to unsubscribe from Defaults to `changed`. |

#### Output

| **Output** | **Description** |
|----------|-----------------|
| `void`   | Unsubscribes the callback from the specified event in the datasource. |

#### Usage Example
```tsx
const exampleDatasource = new datasources.DataSource();
const exampleCallback = () => console.log('Datasource changed!');
unsubscribeFromDatasource(exampleDatasource, exampleCallback);
// The exampleCallback will no longer be invoked on datasource changes.
```




<!-- ################################################################################################################
################################################ DataLoader.ts ######################################################
#####################################################################################################################
-->

## DataLoader.ts

<!-- ########### class ############ -->
### `DataLoader` Class

#### Purpose

Manages and fetches data pages from a given datasource. This class encapsulates the logic for retrieving paginated data and handling changes in the underlying datasource.

#### Properties

- `curpage`: An array representing the current page of data.
- `curstart`: The starting index of the current data page.
- `curend`: The ending index of the current data page.
- `fullLength`: The total length of the data available in the datasource.

#### Constructor

```tsx
constructor(
  private datasource: datasources.DataSource,
  public attributes: string[],
) {}
```

The constructor initializes the `DataLoader` with a specific `datasource` and an array of `attributes` representing the fields to be retrieved.

<!-- ########### create ############ -->
#### Static `create` Method

```tsx
static create(datasource: datasources.DataSource, attributes: string[]) {
  if (['entitysel', 'scalar'].includes(datasource.type))
    return new DataLoader(datasource, attributes);
  return null;
}
```

A static factory method that creates a new `DataLoader` instance based on the type of the datasource. If the datasource is of type `entitysel` or `scalar`, a new `DataLoader` instance is created; otherwise, it returns `null`.

<!-- ########### fetchPage ############ -->
#### `fetchPage` Method

```tsx
async fetchPage(start: number, end: number): Promise<any[]>
```

- Fetches a page of data from the datasource based on the specified start and end indices.
- Trims attributes and retrieves the paginated data, mapping it to a cleaner structure.
- Updates internal properties (`curpage`, `curstart`, `curend`, `fullLength`) based on the fetched data.
- Returns the fetched collection.

<!-- ########### sourceHasChanged ############ -->
#### `sourceHasChanged` Method

```tsx
async sourceHasChanged()
```

- Resets internal properties when the underlying datasource undergoes changes.
- Retrieves the total length of the data and fetches the initial data page if available.

#### Usage Example

```tsx
const datasource = new datasources.DataSource();
const attributes = ['name', 'age', 'city'];
const loader = DataLoader.create(datasource, attributes);

if (loader) {
  const start = 0;
  const end = 10;
  const fetchedData = await loader.fetchPage(start, end);

  // Handling changes in the datasource
  await loader.sourceHasChanged();
}
```


<!-- ################################################################################################################
####################################### datasources-helpers.ts ######################################################
#####################################################################################################################
-->

## datasources-helpers.ts

The `datasources-helpers.ts` file contains utility functions designed to assist with operations involving datasources.

<!-- ########### datasourceQuerySelector ############ -->
### `datasourceQuerySelector` function

#### Purpose
Facilitates the filtering of datasource declarations based on a given query. This function is particularly useful when dealing with multiple datasources and allows selecting specific datasources using a query string.


#### Signature
```tsx
datasourceQuerySelector: (query: string) => (datasource: datasources.ICreateDataSource) => boolean;
```

#### Input

| **Parameter** | **Type** | **Description** |
|---------------|----------|-----------------|
| `query`       | `string` | The query string specifying datasource paths separated by commas. |

#### Output

| **Output** | **Description** |
|----------|-----------------|
| `(datasource: datasources.ICreateDataSource) => boolean`| A filter function that takes a datasource declaration and returns a boolean based on whether it matches the specified paths in the query. |

#### Usage Example
```tsx
const query = 'namespace1:datasource1.id1,namespace2:datasource2.id2';
const filterFunction = datasourceQuerySelector(query);

const datasourcesList: datasources.ICreateDataSource[] = [
  { id: 'id1', namespace: 'namespace1' },
  { id: 'id2', namespace: 'namespace2' },
  { id: 'id3', namespace: 'namespace3' },
];

const filteredDatasources = datasourcesList.filter(filterFunction);
/* Result:
[
  { id: 'id1', namespace: 'namespace1' },
  { id: 'id2', namespace: 'namespace2' },
]
*/
```

In this example, the `datasourceQuerySelector` function is utilized to create a filter function based on the provided query string. This filter function is then applied to a list of datasource declarations, resulting in a filtered list of datasources that match the specified paths in the query.



<!-- ################################################################################################################
################################################ date-utils.ts ######################################################
#####################################################################################################################
-->

## date-utils.ts

The `date-utils.ts` file provides utility functions for formatting and parsing date values. It leverages the `date-fns` library for parsing dates and the `@ws-ui/formatter` library for formatting.

<!-- ########### formatValue ############ -->
### `formatValue` Function

#### Purpose
Formats a date value according to the specified type and format.

#### Signature
```tsx
formatValue(value: number | string | Date, type: string, format?: string): string
```

#### Input

| **Parameter** | **Type** | **Description** |
|---------------|----------|-----------------|
| `value`       | `number`, `string`, `Date` | The date value to be formatted. |
| `type`        | `string` | The type of formatting to apply. |
| `format`      | `string` | (Optional) The format string to be applied. |

#### Output

| **Output** | **Description** |
|----------|-----------------|
| `string` | The formatted date string. |

#### Usage Example
```tsx
const formattedDate = formatValue('01-01-2023', 'string', 'yyyy-MM-dd');
/* Result: 2023-01-01 */
```

<!-- ########### parseValue ############ -->
### `parseValue` Function

#### Purpose
Parses a date value from a number, string, or existing Date object.

#### Signature
```tsx
parseValue<T>(value: number | string | Date | T, format?: string): Date
```

#### Input

| **Parameter** | **Type** | **Description** |
|---------------|----------|-----------------|
| `value`       | `number`, `string`, `Date`, `T` | The value to be parsed as a date. |
| `format`      | `string` | (Optional) The format string to guide the parsing. |

#### Output

| **Output** | **Description** |
|----------|-----------------|
| `Date`   | The parsed date object. |

#### Usage Example
```tsx
const parsedDate = parseValue('01-01-2023', 'yyyy-MM-dd');
/* Result: January 1, 2023 */
```

<!-- ################################################################################################################
################################################ Graph.ts ###########################################################
#####################################################################################################################
-->

## Graph.ts

The `Graph.ts` file provides functionality for topologically sorting datasources based on their dependencies. It ensures that datasources are processed in the correct order, considering dependencies between them.


<!-- ########### class ############ -->
### `Graph` Class

#### Purpose
Implements a simple graph structure to represent dependencies between datasources.

#### Properties
- `adjList`: A record storing the adjacency list for each vertex in the graph.

#### Constructor
```tsx
constructor() {
  this.adjList = {};
}
```
The constructor initializes an empty adjacency list for the graph.

#### `addVertex` Method

##### Signature
```tsx
addVertex(v: string): void;
```

##### Input

| **Parameter** | **Type** | **Description** |
|---------------|----------|-----------------|
| `v`           | `string` | The vertex to be added to the graph. |

#### `addEdge` Method

##### Signature
```tsx
addEdge(v1: string, v2: string): void;
```

##### Input

| **Parameter** | **Type** | **Description** |
|---------------|----------|-----------------|
| `v1`          | `string` | The starting vertex of the edge. |
| `v2`          | `string` | The ending vertex of the edge. |

<!-- ########### sortByDependency ############ -->
### `sortByDependency` Function

#### Purpose
Sorts an array of datasource declarations based on their dependencies.

#### Signature
```tsx
sortByDependency = (
  datasources: datasources.ICreateDataSource[],
): datasources.ICreateDataSource[];
```

#### Input

| **Parameter** | **Type** | **Description** |
|---------------|----------|-----------------|
| `datasources` | `datasources.ICreateDataSource[]` | An array of datasource declarations to be sorted based on dependencies. |

#### Output

| **Output** | **Description** |
|----------|-----------------|
| `datasources.ICreateDataSource[]` | Returns a new array of datasources sorted in the correct order based on their dependencies. |

#### Usage Example
```tsx
const unsortedDatasources: datasources.ICreateDataSource[] = [...]; // Provide your unsorted datasources
const sortedDatasources = sortByDependency(unsortedDatasources);
```

<!-- ########### generateDependencyGraph ############ -->
### `generateDependencyGraph` Function

#### Purpose
Generates a dependency graph based on the provided datasources.

#### Signature
```tsx
generateDependencyGraph(datasources: datasources.ICreateDataSource[]): Graph;
```

#### Input

| **Parameter** | **Type** | **Description** |
|---------------|----------|-----------------|
| `datasources` | `datasources.ICreateDataSource[]` | An array of datasource declarations. |

#### Output

| **Output** | **Description** |
|----------|-----------------|
| `Graph`   | Returns an instance of the `Graph` class representing the dependency graph. |

#### Usage Example
```tsx
const datasources: datasources.ICreateDataSource[] = [...]; // Provide your datasources
const graph = generateDependencyGraph(datasources);
```

<!-- ########### depthFirstTopologicalSort ############ -->
### `depthFirstTopologicalSort` Function

#### Purpose
Performs a depth-first topological sort on the dependency graph.

#### Signature
```tsx
depthFirstTopologicalSort(
  vertex: string,
  n: number,
  visited: Record<string, boolean>,
  orderMap: Record<string, number>,
  adjList: Record<string, string[]>,
  recStack: string[] = [],
): number;
```

#### Input

| **Parameter** | **Type** | **Description** |
|---------------|----------|-----------------|
| `vertex`      | `string` | The current vertex being processed. |
| `n`           | `number` | The depth of the recursion. |
| `visited`     | `Record<string, boolean>` | A record of visited vertices. |
| `orderMap`    | `Record<string, number>` | A record to store the topological order of vertices. |
| `adjList`     | `Record<string, string[]>` | The adjacency list representing the graph. |
| `recStack`    | `string[]` | A stack to detect cycles in the graph. |

#### Output

| **Output** | **Description** |
|----------|-----------------|
| `number` | Returns the updated depth value after processing the current vertex in the topological sort. |

#### Usage Example
```tsx
const datasources: datasources.ICreateDataSource[] = [...]; // Provide your datasources
const graph = generateDependencyGraph(datasources);

const visited: Record<string, boolean> = {};
const orderMap: Record<string, number> = {};
const recStack: string[] = [];
let n = datasources.length;

datasources.forEach((ds) => {
  if (!visited[ds.id]) {
    n = depthFirstTopologicalSort(
      ds.id,
      n,
      visited,
      orderMap,
      graph.adjList,
      recStack,
    );
  }
});

// orderMap now contains the topological order of datasources
```


<!-- ################################################################################################################
#################################################### misc.ts ######################################################
#####################################################################################################################
-->

## misc.ts

The `misc.ts` file encompasses a collection of miscellaneous utility functions designed to handle diverse tasks across the project. These functions are crafted to enhance code readability, maintainability, and provide convenient tools for specific operations.

<!-- ########### parseWebForm ############ -->
### `parseWebForm` Function

#### Purpose
Parses a web form represented as a JSON string and returns a structured object.

#### Signature
```tsx
parseWebForm(webform: string): { [key: string]: NodeData };
```

#### Input

| **Parameter** | **Type** | **Description** |
|---------------|----------|-----------------|
| `webform`     | `string` | A JSON string representing the web form structure. |

#### Output

| **Output** | **Description** |
|----------|-----------------|
| `{ [key: string]: NodeData }` | Returns an object where keys are identifiers and values are `NodeData` objects representing the web form structure. |

#### Usage Example
```tsx
const webformString = '{"id1": { "props": { "text": "Sample Text" }}}';
const parsedWebForm = parseWebForm(webformString);
/* Result: 
{
  "id1": {
    "props": {
      "text": "Sample Text"
    }
  }
}
*/
```

<!-- ########### sanitizeStyle ############ -->
### `sanitizeStyle` Function

#### Purpose
Sanitizes a `CSSProperties` object by removing unset properties for better behavior.

#### Signature
```tsx
sanitizeStyle(style: CSSProperties | undefined): CSSProperties;
```

#### Input

| **Parameter** | **Type** | **Description** |
|---------------|----------|-----------------|
| `style`       | `CSSProperties` \| `undefined` | The style object to be sanitized. |

#### Output

| **Output** | **Description** |
|----------|-----------------|
| `CSSProperties` | Returns a sanitized `CSSProperties` object. |

#### Usage Example
```tsx
const inputStyle = { color: 'red', fontSize: '', margin: '10px' };
const sanitizedStyle = sanitizeStyle(inputStyle);
/* Result: 
{
  "color": "red",
  "margin": "10px"
}
*/
```

<!-- ########### capitalizeFirstLetter ############ -->
### `capitalizeFirstLetter` Function

#### Purpose
Capitalizes the first letter of a string.

#### Signature
```tsx
capitalizeFirstLetter(str: string): string;
```

#### Input

| **Parameter** | **Type** | **Description** |
|---------------|----------|-----------------|
| `str`         | `string` | The input string to be capitalized. |

#### Output

| **Output** | **Description** |
|----------|-----------------|
| `string` | Returns the input string with the first letter capitalized. |

#### Usage Example
```tsx
const inputString = 'example';
const capitalizedString = capitalizeFirstLetter(inputString);
/* Result: Example*/
```


<!-- ################################################################################################################
########################################## numToMeasurement.ts ######################################################
#####################################################################################################################
-->

## numToMeasurement.ts

The `numToMeasurement.ts` file provides utility functions related to numerical-to-measurement conversions and obtaining element dimensions.

<!-- ########### isPercentage ############ -->
### `isPercentage` Function

#### Purpose
Determines if a given value is a percentage string.

#### Signature
```tsx
isPercentage(val: string): boolean;
```

#### Input

| **Parameter** | **Type** | **Description** |
|---------------|----------|-----------------|
| `val`         | `string` | The value to be checked. |

#### Output

| **Output** | **Description** |
|----------|-----------------|
| `boolean` | Returns `true` if the input is a percentage string, otherwise `false`. |

#### Usage Example
```tsx
const result = isPercentage('50%');
/* Result: true */
```

<!-- ########### percentToPx ############ -->
### `percentToPx` Function

#### Purpose
Converts a percentage value to pixels based on a comparative value.

#### Signature
```tsx
percentToPx(value: any, comparativeValue: number): string | any;
```

#### Input

| **Parameter** | **Type** | **Description** |
|---------------|----------|-----------------|
| `value`       | `any`    | The value to be converted. |
| `comparativeValue` | `number` | The reference value for the conversion. |

#### Output

| **Output** | **Description** |
|----------|-----------------|
| `string` \| `any` | Returns the value in pixels if it's a percentage, 'auto', or has no comparative value; otherwise, returns the original value. |

#### Usage Example
```tsx
const result = percentToPx('50%', 200);
/* Result: '100px' */
```

<!-- ########### pxToPercent ############ -->
### `pxToPercent` Function

#### Purpose
Converts a pixel value to a percentage based on a comparative value.

#### Signature
```tsx
pxToPercent(value: any, comparativeValue: number): number;
```

#### Input

| **Parameter** | **Type** | **Description** |
|---------------|----------|-----------------|
| `value`       | `any`    | The value to be converted. |
| `comparativeValue` | `number` | The reference value for the conversion. |

#### Output

| **Output** | **Description** |
|----------|-----------------|
| `number` | Returns the value as a percentage. |

#### Usage Example
```tsx
const result = pxToPercent(100, 200);
/* Result: 50 */
```

<!-- ########### getElementDimensions ############ -->
### `getElementDimensions` Function

#### Purpose
Obtains the dimensions (width and height) of an HTML element, accounting for padding.

#### Signature
```tsx
getElementDimensions(element: HTMLElement): { width: number; height: number };
```

#### Input

| **Parameter** | **Type** | **Description** |
|---------------|----------|-----------------|
| `element`     | `HTMLElement` | The HTML element for which dimensions are to be obtained. |

#### Output

| **Output** | **Description** |
|----------|-----------------|
| `{ width: number; height: number }` | Returns an object containing the width and height of the specified element, excluding padding. |

#### Usage Example
```tsx
const element = document.getElementById('exampleElement');
const dimensions = getElementDimensions(element);
/* Result: { width: 200, height: 150 } */
```


<!-- ################################################################################################################
######################################### PopoverComponents.ts ######################################################
#####################################################################################################################
-->

## PopoverComponents.tsx

The `PopoverComponents.tsx` file contains React components related to popovers.

<!-- ########### PopoverBody ############ -->
### `PopoverBody` Component

#### Purpose
Represents the body of a popover, typically containing content or controls.

#### Properties
- `children`: Content to be displayed within the popover body.

#### Usage Example
```tsx
<PopoverBody>
  <p>This is the content of the popover body.</p>
</PopoverBody>
```
s
<!-- ########### PopoverButton ############ -->
### `PopoverButton` Component

#### Purpose
Represents a button within a popover, styled based on the specified variant.

#### Properties
- `onClick`: Mouse event handler for the button click.
- `label`: Text content of the button.
- `icon`: tsx element representing an icon.
- `variant`: Button variant ('primary', 'confirm', 'error').
- `disabled`: Boolean indicating whether the button is disabled.
- `className`: Additional class names for styling.

#### Usage Example
```tsx
<PopoverButton
  onClick={() => console.log('Button clicked')}
  label="Submit"
  variant="primary"
/>
```

<!-- ########### PopoverField ############ -->
### `PopoverField` Component

#### Purpose
Represents a field within a popover, typically used for grouping content.

#### Properties
- `children`: Content to be displayed within the popover field.

#### Usage Example
```tsx
<PopoverField>
  <p>This is the content of the popover field.</p>
</PopoverField>
```

<!-- ########### PopoverInput ############ -->
### `PopoverInput` Component

#### Purpose
Represents an input field within a popover, with optional error messaging.

#### Properties
- `value`: Current value of the input.
- `onChange`: Function called on input change.
- `onKeyDown`: Keyboard event handler.
- `onPaste`: Clipboard event handler.
- `type`: Input type ('number' or 'text').
- `min`: Minimum value for a numeric input.
- `max`: Maximum value for a numeric input.
- `placeholder`: Placeholder text for the input.
- `error`: Error message to be displayed.
- `autoFocus`: Boolean indicating autofocus.
- `onFocus`: Function called on input focus.
- `onBlur`: Function called on input blur.

#### Usage Example

```tsx
<PopoverInput
    value={inputValue}
    onChange={(value) => setInputValue(value)}
    type="text"
    placeholder="Enter text"
    error="Invalid input"
/>
```

<!-- ########### PopoverCombox ############ -->
### `PopoverCombox` Component

#### Purpose
Represents a combo box within a popover, allowing selection from suggestions.

#### Properties
- `value`: Current selected value.
- `onChange`: Function called on value change.
- `placeholder`: Placeholder text for the combo box.
- `error`: Error message to be displayed.
- `suggestions`: Array of suggestions.

#### Example Usage
```tsx
<PopoverCombox
    value={comboValue}
    onChange={(value) => setComboValue(value)}
    placeholder="Select an option"
    error="Invalid selection"
    suggestions={['Option 1', 'Option 2', 'Option 3']}
/>
```


<!-- ########### PopoverSelect ############ -->
### `PopoverSelect` Component

#### Purpose
Represents a select dropdown within a popover.

#### Properties
- `value`: Current value of the select dropdown.
- `onChange`: Function called on select dropdown value change.
- `placeholder`: Placeholder text for the select dropdown.
- `options`: Array of option objects with `value` and `label`.
- `disabled`: Boolean indicating whether the select dropdown is disabled.
- `error`: Error message to display.
- `className`: Additional class names for styling.

#### Usage Example

```tsx
<PopoverSelect
    value={selectedValue}
    onChange={(value) => setSelectedValue(value)}
    placeholder="Select an option"
    options={[
        { value: '1', label: 'Option 1' },
        { value: '2', label: 'Option 2' },
        { value: '3', label: 'Option 3' },
    ]}
    disabled={false}
    error="Invalid selection"
/>
```

<!-- ########### PopoverTooltip ############ -->
### `PopoverTooltip` Component

#### Purpose
Represents a tooltip within a popover, displaying additional information.

#### Properties
- `content`: Tooltip content.
- `side`: Tooltip position ('top', 'bottom', 'left', 'right').
- `hasArrow`: Boolean indicating whether the tooltip has an arrow.
- `className`: Additional class names for styling.

#### Example Usage
```tsx
<PopoverTooltip content="This is a tooltip" side="top" hasArrow={true}>
  <button>Hover me</button>
</PopoverTooltip>
```

:::info
Please note that these components are assumed to be used within a popover context and might require additional styling based on your application's design.
:::

<!-- ################################################################################################################
########################################## renderComponents.ts ######################################################
#####################################################################################################################
-->

## renderComponents.ts

The `renderComponents.ts` file provides a function for rendering components based on a given array of settings.

<!-- ########### renderComponents ############ -->
### `renderComponents` Function

#### Purpose
Renders React components based on an array of setting objects.

#### Signature
```tsx
renderComponents(components: TSetting[], map?: Record<string, React.FC<any>>): any;
```

#### Input

| **Parameter** | **Type** | **Description** |
|---------------|----------|-----------------|
| `components`  | `TSetting[]` | An array of setting objects. |
| `map`         | `Record<string, React.FC>` | An optional map object for custom component mappings. |

#### Output

| **Output** | **Description** |
|----------|-----------------|
| `any`    | An array of React components based on the provided settings. |

#### Usage Example
```tsx
const components = [
  { type: ESetting.TEXT_FIELD, label: 'Name', key: 'name' },
  { type: ESetting.GROUP, components: [{ type: ESetting.COLOR_PICKER, key: 'color' }] },
  // ... other settings
];

const renderedComponents = renderComponents(components);
/* Result:
[
  React.createElement(Textfield, { label: 'Name', key: 'name' }),
  React.createElement(Group, {
    components: [React.createElement(ColorPicker, { key: 'color' })],
  }),
  // ... other rendered components
]
*/
```

<!-- ################################################################################################################
########################################## searchComponents.ts ######################################################
#####################################################################################################################
-->

## searchComponents.ts

<!-- ########### searchComponents ############ -->
### `searchComponents` Function

#### Purpose
Searches for components within a tree-like structure based on a search value.

#### Signature
```tsx
searchComponents(components: any, searchValue: any): any[];
```

#### Input

| **Parameter**  | **Type** | **Description**         |
|----------------|----------|-------------------------|
| `components`   | `any`    | The tree-like structure of components. |
| `searchValue`  | `any`    | The value to search for within the components. |

#### Output

| **Output**  | **Description**                 |
|-----------|---------------------------------|
| `any[]`   | An array of components that match the search criteria. |

#### Usage Example
```tsx
const searchResult = searchComponents(components, 'searchValue');
/* Result: Array of components matching the search criteria */
```


<!-- ################################################################################################################
########################################### settingsComponent.ts ####################################################
#####################################################################################################################
-->

## settingsComponent.tsx

<!-- ########### Settings ############ -->
### `Settings` Function

#### Purpose
Returns a functional component that renders the settings components based on the current mode and search criteria.

#### Signature
```tsx
Settings(
  settingsComponents: TSetting[],
  basicSettings?: TSetting[]
): React.ElementType;
```

#### Input

| **Parameter**          | **Type** | **Description**                                                        |
|------------------------|----------|------------------------------------------------------------------------|
| `settingsComponents`   | `TSetting[]` | An array of all settings components, including advanced settings.    |
| `basicSettings`        | `TSetting[]` | An optional array of basic settings to be displayed in basic mode.    |

#### Output

| **Output**       | **Description**                        |
|----------------|----------------------------------------|
| `React.ElementType` | The component that renders the settings based on the current mode and search criteria. |

#### Usage Example
```tsx
const SettingsComponent = Settings(allSettings, basicSettings);
/* Result: A React component for rendering settings. */
```


<!-- ################################################################################################################
########################################## settingsDefaults.ts ######################################################
#####################################################################################################################
-->

## settingsDefaults.ts

<!-- ########### load ############ -->
### `load` Function

#### Purpose
Loads and provides utility functions for handling web form settings.

#### Signature
```tsx
load(settings?: TSetting[]): {
  DEFAULT_SETTINGS: TSetting[];
  filter(...keys: string[]): TSetting[];
  replace(key: string, payload: TSetting): TSetting[];
};
```

#### Input

| **Parameter** | **Type** | **Description**                                        |
|---------------|----------|--------------------------------------------------------|
| `settings`    | `TSetting[]` | An optional array of web form settings. Defaults to `DEFAULT_SETTINGS`. |

#### Output

| **Output**       | **Description**                                        |
|----------------|--------------------------------------------------------|
| `{ DEFAULT_SETTINGS, filter, replace }` | An object containing default settings, a filter function, and a replace function. |

#### Usage Example
```tsx
const { DEFAULT_SETTINGS, filter, replace } = load();
/* Result: An object with default settings, filter, and replace functions. */
```

- `DEFAULT_SETTINGS`: An array of default web form settings.
- `filter(...keys: string[]): TSetting[]`: Filters settings based on the provided keys.
- `replace(key: string, payload: TSetting): TSetting[]`: Replaces a setting with the provided payload.



<!-- ################################################################################################################
################################################## subjects.ts ######################################################
#####################################################################################################################
-->

<!-- test -->



<!-- ################################################################################################################
################################################# testUtils.ts ######################################################
#####################################################################################################################
-->

## testUtils.tsx

<!-- ########### configureStore ############ -->
### `configureStore` Function

#### Purpose
A function that configures and creates a Redux store.

#### Signature
```tsx
configureStore(options: {
  reducer: Record<string, any>;
}): Store;
```

#### Input

| **Parameter** | **Type** | **Description** |
|---------------|----------|-----------------|
| `options`     | `object` | Configuration options for the store. |
| `options.reducer` | `Record<string, any>` | The root reducer for the store. |

#### Output
A Redux store.

#### Example
```tsx
const store = configureStore({
  reducer: {
    root: rootReducer,
  },
});
/* Result: A configured Redux store. */
```

<!-- ########### createEditorComponent ############ -->
### `createEditorComponent` Function

#### Purpose
A function that creates an editor component with a specified component.

#### Signature
```tsx
createEditorComponent(Component: T4DComponent): JSX.Element;
```

#### Input

| **Parameter** | **Type** | **Description** |
|---------------|----------|-----------------|
| `Component`   | `T4DComponent` | The component to be used in the editor. |

#### Output
A JSX element representing the editor with the specified component.

#### Example
```tsx
const editorComponent = createEditorComponent(MyComponent);
/* Result: A JSX element representing the editor with `MyComponent`. */
```
