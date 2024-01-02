---
id: hooks
title: Hooks
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

## Overview

The directory structure for the **hooks** folder outlines:

- **hooks**
    - **use-dnd-handler**:
        - [**helpers.ts**](#use-dnd-handlerhelpersts): Helper functions for drag-and-drop handling.
        - [**index.tsx**](#use-dnd-handlerindextsx): Entry point exporting hook functions.
        - [**type-guards.ts**](#use-dnd-handlertype-guardsts): Type guards for drag-and-drop operations.
        - [**types.ts**](#use-dnd-handlertypests): Type definitions related to drag-and-drop.
    - **use-dnd-scope**:
        - [**index.tsx**](#use-dnd-scopeindextsx): Main implementation for creating a drag-and-drop scope.
    - **use-emit**:
        - [**index.tsx**](#use-emitindextsx): Hook for emitting events.
        - [**utils.tsx**](#use-emitutilstsx): Utility functions related to event emission.
    - **use-enhanced-layer**:
        - [**use-enhanced-layers.tsx**](#use-enhanced-layeruse-enhanced-layerstsx): Hook for managing enhanced layers in an editor.
    - **use-enhanced-node**:
        - [**adapters.ts**](#use-enhanced-nodeadapterstsx): Adapters for enhanced node functionality.
        - [**drop-indicator.tsx**](#use-enhanced-nodedrop-indicatortsx): Drop indicator component.
        - [**index.tsx**](#use-enhanced-nodeindextsx): Main implementation for enhanced node handling.
    - **use-sources**:
        - [**index.tsx**](#use-sourcesindextsx): Hook for managing data sources.
    - [**events-selector.tsx**](#events-selectortsx): Selector for events in the application.
    - [**use-datasource-adapter.ts**](#use-datasource-adapterts): Hook for adapting data sources.
    - [**use-datasources-subscription.ts**](#use-datasources-subscriptionts): Hook for subscribing to data sources.
    - [**use-delayed-state.ts**](#use-delayed-statets): Hook for managing delayed state updates.
    - [**use-ds-autosuggest.ts**](#use-ds-autosuggestts): Hook for handling auto-suggestions in data sources.
    - [**use-editor-helpers.ts**](#use-editor-helpersts): Hook providing helper functions for editors.
    - [**use-enhanced-editor.ts**](#use-enhanced-editorts): Hook for enhancing the functionality of an editor.
    - [**use-events-adapter.ts**](#use-events-adapterts): Hook for adapting and handling events.
    - [**use-forwarded-ref.ts**](#use-forwarded-refts): Hook for forwarding references.
    - [**use-iterable-parent-node.ts**](#use-iterable-parent-nodets): Hook for managing iterable parent nodes.
    - [**use-layout.ts**](#use-layoutts): Hook for managing layout configurations.
    - [**use-methods.ts**](#use-methodsts): Hook for handling methods in the application.
    - [**use-node-datasource.ts**](#use-node-datasourcets): Hook for managing data sources at the node level.
    - [**use-node-tree.ts**](#use-node-treets): Hook for managing the tree structure of nodes.
    - [**use-parent-node-child.ts**](#use-parent-node-childts): Hook for managing child nodes of a parent node.
    - [**use-parent-node-props.ts**](#use-parent-node-propsts): Hook for managing properties of parent nodes.
    - [**use-renderer.ts**](#use-rendererts): Hook for rendering components.
    - [**use-studio-panel.ts**](#use-studio-panelts): Hook for managing the studio panel.
    - [**use-style-adapter.ts**](#use-style-adapterts): Hook for adapting styles.
    - [**use-synced-state.ts**](#use-synced-statets): Hook for managing synchronized state.
    - [**use-welcome-tour-flags.ts**](#use-welcome-tour-flagsts): Hook for handling welcome tour flags.



<!-- ################################################################################################################
################################### use-dnd-handler/helpers.ts ######################################################
#####################################################################################################################
-->

## use-dnd-handler/helpers.ts




<!-- ################################################################################################################
#################################### use-dnd-handler/index.tsx ######################################################
#####################################################################################################################
-->

## use-dnd-handler/index.tsx




<!-- ################################################################################################################
############################### use-dnd-handler/type-guards.ts ######################################################
#####################################################################################################################
-->

## use-dnd-handler/type-guards.ts




<!-- ################################################################################################################
##################################### use-dnd-handler/types.ts ######################################################
#####################################################################################################################
-->

## use-dnd-handler/types.ts




<!-- ################################################################################################################
###################################### use-dnd-scope/index.tsx ######################################################
#####################################################################################################################
-->

## use-dnd-scope/index.tsx 








<!-- ################################################################################################################
########################################### use-emit/index.tsx ######################################################
#####################################################################################################################
-->

## use-emit/index.tsx

<!-- ########### useEmit ############ -->
### `useEmit` Function

#### Purpose
A hook that provides methods and state information to emit events in a webform.

#### Signature
```tsx
useEmit(options?: UseEmitOptions): {
  emit: TEmit;
  eventsToHandle: TEvents;
};
```

#### Input

| **Parameter**  | **Type** | **Description**         |
|----------------|----------|-------------------------|
| `props` (Optional) | `UseEmitOptions` | Configuration options for the useEmit hook, including `enabled` and `omittedEvents`. |

:::info
The `useEmit` hook takes an optional configuration object (`UseEmitOptions`) with properties:

- **enabled** (boolean, default: false): Indicates whether the emit functionality is enabled.

- **omittedEvents** (string[], default: []): An array of event names to be omitted during emission.
:::

#### Output

| **Output**  | **Description**                 |
|-------------|---------------------------------|
| `UseEmitReturn`   | An object containing the [`emit`](#emit) function and [`eventsToHandle`](#eventstohandle) object. |


#### Properties

##### `emit`

| **Type** | **Description** |
|----------|-----------------|
| [`TEmit`](#temit) | A function that emits events in the webform. |

##### `eventsToHandle`

| **Type** | **Description** |
|----------|-----------------|
| [`TEvents`](#tevents) | An object containing event handler functions for supported events. |

#### Types

##### `TEmit`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `eventName` (string), `event` (T) (Optional) | `Promise<void>` | Emits an event in the webform. If `event` is provided, it includes additional data to be sent with the event. The method returns a promise that resolves once the event emission is completed. |

##### `TEvents`

| **Type** | **Description** |
|----------|-----------------|
| `Object` | An object containing event handler functions for supported events. The keys are the names of the events, and the values are the corresponding event handler functions. These functions are automatically bound to the associated events in the webform. |

#### Usage Example

<Tabs>
<TabItem value="Example 1">
Basic usage:

```tsx
import { useEmit } from "@ws-ui/webform-editor";

const BasicComponent = () => {
  // highlight-next-line
  const { emit, eventsToHandle } = useEmit();

  return (
    <div>
      <p>Connected Events:</p>
      {Object.keys(eventsToHandle).map((eventName) => (
        <div key={eventName}>{eventName}</div>
      ))}

      <button onClick={() => emit('onClick')}>Trigger Click Event</button>
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 2">
Customized omitted events:

```tsx
import { useEmit } from "@ws-ui/webform-editor";

const CustomizedOmittedEventsComponent = () => {
  // highlight-next-line
  const { emit, eventsToHandle } = useEmit({ omittedEvents: ['onFocus', 'onBlur'] });

  return (
    <div>
      <p>Connected Events (excluding onFocus and onBlur):</p>
      {Object.keys(eventsToHandle).map((eventName) => (
        <div key={eventName}>{eventName}</div>
      ))}

      <button onClick={() => emit('onClick')}>Trigger Click Event</button>
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 3">
Disabled auto-Binding:

```tsx
import { useEmit } from "@ws-ui/webform-editor";

const DisabledAutoBindComponent = () => {
  // highlight-next-line
  const { emit, eventsToHandle } = useEmit({ autoBindEvents: false });

  return (
    <div>
      <p>Events are not auto-bound:</p>

      <button onClick={() => emit('onClick')}>Trigger Click Event</button>
    </div>
  );
};
```

</TabItem>

</Tabs>







<!-- ################################################################################################################
#################################################### use-emit/utils.tsx ######################################################
#####################################################################################################################
-->



## use-emit/utils.tsx 

<!-- ########### executeEvents ############ -->
### `executeEvents` Function

#### Purpose

A hook that handles the execution of events in the context of a web form. It supports various types of events, including navigation, method execution, and simple actions. The function processes events one by one and provides feedback messages through toasts.

#### Signature

```tsx
executeEvents({
  eventName: string;
  events: webforms.WEvent[];
  id: string;
  compRef?: string;
  additionalData?: any;
  getIteratorDatasource?: (source: string) => TIteratorDatasource | undefined;
  namespace: string;
  rendererUrl: string;
  navigateTo: (webform: string) => void;
  isOutsideWebformLoader?: boolean;
  isInsideStudio?: boolean;
  toast?: ReturnType<typeof useToast>;
}): Promise<void>;
```

#### Input

| **Parameter**      | **Type**             | **Description**             |
|--------------------------|------------------|------------------------|
| `eventName`              | `string`            | The name of the event to execute.                            |
| `events`                 | `webforms.WEvent[]` | List of events associated with the specified event name.     |
| `id`                     | `string`            | Caller ID.                                                   |
| `compRef`                | `string`            | Component reference.                                         |
| `additionalData`         | `any`               | Additional data to be sent with the request to the server.   |
| `getIteratorDatasource`  | `(source: string) => TIteratorDatasource` \| `undefined` | Getter function for the current iterator datasource.  |
| `namespace`              | `string`            | The datasource namespace.                                                               |
| `rendererUrl`            | `string`            | The renderer URL.                                                                       |
| `navigateTo`             | `(webform: string) => void`  | Navigation callback function.                      |
| `isOutsideWebformLoader` | `boolean`           | A boolean indicating if the event was executed from outside of a webform loader.        |
| `isInsideStudio`         | `boolean`           | A boolean indicating if the event was executed from inside the webstudio.               |
| `toast`                  | `ReturnType<typeof useToast>`                | Toast callback function from Chakra UI.         |

#### Output

| **Output**  | **Description** |
|-------------|-----------------|
| `Promise<void>` | A promise that resolves when all events are executed, or rejects if an error occurs. |


#### Usage Example

```tsx
import { executeEvents } from '@ws-ui/webform-editor';
import { useToast } from '@chakra-ui/react';

const BasicComponent = () => {
  const namespace = 'yourNamespace';
  const rendererUrl = 'yourRendererUrl';
  const navigateTo = (webform: string) => /* your navigateTo implementation */;
  const toast = useToast();

  // Execute events for a specific event name
  // highlight-next-line
  executeEvents({
    eventName: 'yourEventName',
    events: yourEventsArray,
    id: 'yourUniqueId',
    namespace,
    rendererUrl,
    navigateTo,
    toast,
  });
};
```


<!-- ########### getDatasourceValue ############ -->
### `getDatasourceValue` Helper Function

#### Purpose

A utility function that retrieves the value of a datasource given its source and namespace.

#### Signature

```tsx
getDatasourceValue(source: webforms.QueryParam['datasource'], path: string): Promise<string>;
```

#### Input

| **Parameter** | **Type**                             | **Description**                                                    |
|---------------|--------------------------------------|--------------------------------------------------------------------|
| `source`      | `webforms.QueryParam['datasource']`   | The datasource source to retrieve the value from.                   |
| `path`        | `string`                             | The datasource namespace.                                           |

#### Output

| **Output** | **Description**                                           |
|------------|-----------------------------------------------------------|
| `Promise<string>` | A promise that resolves to the value of the datasource. |



<!-- ########### getActionMeta ############ -->
### `getActionMeta` Helper Function

#### Purpose

A utility function that generates metadata for a simple action event.

#### Signature

```tsx
getActionMeta(
  { action, query, orderBy }: webforms.SimpleActionEvent,
  path: string,
): Promise<any>;
```

#### Input

| **Parameter** | **Type**                               | **Description**                                           |
|---------------|----------------------------------------|-----------------------------------------------------------|
| `action`      | `webforms.SimpleActionEvent['action']` | The type of action to generate metadata for.               |
| `query`       | `webforms.SimpleActionEvent['query']`  | The query object for the action (used for 'query' action). |
| `orderBy`     | `webforms.SimpleActionEvent['orderBy']`| The orderBy parameter for the action (used for 'orderBy' action). |
| `path`        | `string`                               | The datasource namespace.                                   |

#### Output

| **Output** | **Description**                                               |
|------------|---------------------------------------------------------------|
| `Promise<any>` | A promise that resolves to the generated metadata for the action. |



<!-- ########### getEventsMap ############ -->
### `getEventsMap` Helper Function

#### Purpose

A utility function that populates an event map with events for each event name.

#### Signature

```tsx
getEventsMap(events: webforms.WEvent[]): Map<string, webforms.WEvent[]>;
```

#### Input

| **Parameter** | **Type**             | **Description**                                           |
|---------------|----------------------|-----------------------------------------------------------|
| `events`      | `webforms.WEvent[]`  | List of events to populate the event map with.             |

#### Output

| **Output** | **Description**                                               |
|------------|---------------------------------------------------------------|
| `Map<string, webforms.WEvent[]>` | A map where keys are event names, and values are lists of associated events. |






<!-- ################################################################################################################
#################################### use-enhanced-layer/use-enhanced-layers.tsx######################################
#####################################################################################################################
-->

## use-enhanced-layer/use-enhanced-layers.tsx

<!-- ########### useEnhancedLayers ############ -->
### `useEnhancedLayers` Function

#### Purpose
A hook that enhances the functionality of layers in a web form editor using Craft.js. It provides features for handling component drops, managing data transfer, and updating the layers dynamically.

#### Signature
```tsx
useEnhancedLayers(): {
  dom: HTMLElement | null;
  hovered: boolean;
  expanded: boolean;
  connectLayer: (ref: HTMLElement) => void;
};
```

#### Input (N/A)

#### Output

| **Output**                        | **Description**                                     |
|-----------------------------------|-----------------------------------------------------|
| `useEnhancedLayersReturnType`| An object with properties representing the enhanced functionality of a layer in a web form editor.   |

:::info
The `useEnhancedLayers` function returns an object with the following structure:

- **dom**: HTMLElement | null - The DOM element reference of the layer.
- **hovered**: boolean - Indicates whether the layer is currently being hovered.
- **expanded**: boolean - Indicates whether the layer is expanded.
- **connectLayer**: (ref: HTMLElement) => void - A function to connect the layer to its DOM element.
:::

#### Usage Example

<Tabs>
<TabItem value="Example 1">
Basic usage:

```tsx
import { useEnhancedLayers } from '@ws-ui/webform-editor';

const BasicLayerComponent = ({ id, children }) => {
  // highlight-next-line
  const { expanded, connectLayer } = useEnhancedLayers();

  return (
    <div ref={(ref) => ref && connectLayer(ref)}>
      <div>{`Layer ID: ${id}`}</div>
      {expanded && <div>{`Expanded Content for Layer ID: ${id}`}</div>}
      {children}
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 2">
Layer component with conditional rendering:

```tsx
import { useEnhancedLayers } from '@ws-ui/webform-editor';

const ConditionalLayerComponent = ({ id, children }) => {
  // highlight-next-line
  const { expanded, connectLayer } = useEnhancedLayers();

  return (
    <div ref={(ref) => ref && connectLayer(ref)}>
      <div>{`Layer ID: ${id}`}</div>
      {expanded && (
        <div>{`Expanded Content for Layer ID: ${id}`}</div>
      )}
      {children && (
        <div>{`Children Content for Layer ID: ${id}`}</div>
      )}
    </div>
  );
};
```

</TabItem>

</Tabs>


<!-- ################################################################################################################
######################################## use-enhanced-node/adapters.tsx #############################################
#####################################################################################################################
-->

## use-enhanced-node/adapters.tsx

<!-- ########### styleDropHandler ############ -->
### `styleDropHandler` Function

#### Purpose
A hook that handles the drop of styles onto a node in the web form editor.

#### Signature
```tsx
styleDropHandler(
  nodeId: string,
  dataTransfer: IStyleDataTransfer,
  query: useEditorReturnType['query'],
  cssQuery: ReturnType<typeof useStylesEntity>['query'],
): Record<string, ExoProps>;
```

#### Input

| **Name**      | **Type**                         | **Description**                                                   |
|---------------|----------------------------------|-------------------------------------------------------------------|
| `nodeId`      | `string`                         | The ID of the target node where the styles are dropped.           |
| `dataTransfer`| `IStyleDataTransfer`              | The data transfer object containing information about the dropped styles. |
| `query`       | `useEditorReturnType['query']`   | The query function from the web form editor to retrieve information about nodes. |
| `cssQuery`    | `ReturnType<typeof useStylesEntity>['query']` | The query function from the style adapter to retrieve information about CSS classes. |

#### Output

| **Output**                        | **Description**                                     |
|-----------------------------------|-----------------------------------------------------|
| `Record<string, ExoProps>`        | A record of updates to components, where the keys are the component IDs, and the values are the updated props. |

:::info
This function handles the dropping of styles onto a node in the web form editor. It considers various scenarios, including linked nodes and parent-child relationships, to determine the appropriate updates to the components.
:::


#### Usage Example

```tsx
import { styleDropHandler } from '@ws-ui/webform-editor';
import { useEditor } from '@ws-ui/craftjs-core';

const MyComponent = () => {
  const { query } = useEditor();

  const handleStyleDrop = (nodeId, dataTransfer) => {
    const cssQuery = /* ... */; // Set up your CSS query function
    // highlight-next-line
    const updates = styleDropHandler(nodeId, dataTransfer, query, cssQuery);

    // Apply the updates to components
    Object.entries(updates).forEach(([id, props]) => {
      query.node(id).setProps(props);
    });
  };

  return (
    <div
      onDrop={(e) => handleStyleDrop('node123', e.dataTransfer)}
      onDragOver={(e) => e.preventDefault()}
    >
      {/* Your component content */}
    </div>
  );
};
```


<!-- ########### datasourceDropHanlder ############ -->
### `datasourceDropHanlder` Function

#### Purpose
A hook that handles the drop of datasources onto a node in the web form editor.

#### Signature
```tsx
datasourceDropHanlder(
  nodeId: string,
  query: useEditorReturnType['query'],
  dataTransfer: TDSDataTransferPayload,
  iterator?: string,
): Record<string, ExoProps>;
```

#### Input

| **Name**      | **Type**                         | **Description**                                                   |
|---------------|----------------------------------|-------------------------------------------------------------------|
| `nodeId`      | `string`                         | The ID of the target node where the datasource is dropped.         |
| `query`       | `useEditorReturnType['query']`   | The query function from the web form editor to retrieve information about nodes. |
| `dataTransfer`| `TDSDataTransferPayload`         | The data transfer payload containing information about the dropped datasource. |
| `iterator`    | `string, optional`               | An optional iterator parameter.                                   |

#### Output

| **Output**                        | **Description**                                     |
|-----------------------------------|-----------------------------------------------------|
| `Record<string, ExoProps>`        | A record of updates to components, where the keys are the component IDs, and the values are the updated props. |

:::info
This function handles the dropping of datasources onto a node in the web form editor. It updates the datasource prop of the target node with the dropped datasource information.
:::


#### Usage Example

```tsx
import { datasourceDropHanlder, useEnhancedNode } from '@ws-ui/webform-editor';

const NodeComponent = () => {
  const { id, query } = useEnhancedNode();

  const handleDrop = (e) => {
    const dataTransferPayload = /* extract data transfer payload from event */;
    const iterator = /* extract iterator value if available */;
    
    // highlight-next-line
    const updates = datasourceDropHanlder(id, query, dataTransferPayload, iterator);
    
    // Use the updates to apply changes to your components
    // e.g., dispatch an action to update the state with the new props
  };

  return (
    <div onDrop={handleDrop} draggable>
      {/* Your component content */}
    </div>
  );
};
```



<!-- ########### isAcceptedDs ############ -->
### `isAcceptedDs` Function

A hook that determines whether a dropped datasource is accepted based on specified criteria.

#### Signature
```tsx
isAcceptedDs(
  accept: string[],
  payload: TDSDataTransferPayload,
): boolean;
```

#### Input

| **Name**      | **Type**                   | **Description**                                           |
|---------------|----------------------------|-----------------------------------------------------------|
| `accept`      | `string[]`                 | An array of accepted datasource types.                    |
| `payload`     | `TDSDataTransferPayload`   | The data transfer payload containing information about the dropped datasource. |

#### Output

| **Output**  | **Description**                 |
|-------------|---------------------------------|
| `boolean`   | `true` if the datasource is accepted; `false` otherwise. |



<!-- ########### datasourceAcceptance ############ -->
### `datasourceAcceptance` Function

A hook that determines whether a dropped datasource is accepted based on additional criteria.

#### Signature
```tsx
datasourceAcceptance(
  data: TDSDataTransferPayload,
  accept?: string[],
  canAttach?: (payload: TDSDataTransferPayload) => boolean,
  currentDatasource?: datasources.ICreateDataSource | undefined,
): boolean;
```

#### Input

| **Name**              | **Type**                                             | **Description**                                           |
|-----------------------|------------------------------------------------------|-----------------------------------------------------------|
| `data`                | `TDSDataTransferPayload`                             | The data transfer payload containing information about the dropped datasource. |
| `accept` (optional)   | `string[]`                                           | An array of accepted datasource types.                    |
| `canAttach` (optional)| `(payload: TDSDataTransferPayload) => boolean`       | A function to determine if the datasource can be attached. |
| `currentDatasource` (optional)| `datasources.ICreateDataSource | undefined`   | The current datasource, if any, associated with the target node. |

#### Output

| **Output**  | **Description**                 |
|-------------|---------------------------------|
| `boolean`   | `true` if the datasource is accepted; `false` otherwise. |



<!-- ########### getDsTypeFromAttr ############ -->
### `getDsTypeFromAttr` Helper Function

#### Purpose
A helper function that retrieves the datasource type from an attribute.

#### Signature
```tsx
getDsTypeFromAttr(attribute: catalog.IAttribute): string;
```

#### Input

| **Name**      | **Type**                     | **Description**                                           |
|---------------|------------------------------|-----------------------------------------------------------|
| `attribute`   | `catalog.IAttribute`         | The attribute from which to retrieve the datasource type.  |

#### Output

| **Output**  | **Description**                 |
|-------------|---------------------------------|
| `string`    | The datasource type derived from the attribute. |


<!-- ########### isSameDataclass ############ -->
### `isSameDataclass` Helper Function

#### Purpose
A helper function that checks if the dropped datasource belongs to the same dataclass.

#### Signature
```tsx
isSameDataclass(
  data: TDSDataTransferPayload,
  currentDataclass: string,
): boolean;
```

#### Input

| **Name**              | **Type**                   | **Description**                                           |
|-----------------------|----------------------------|-----------------------------------------------------------|
| `data`                | `TDSDataTransferPayload`   | The data transfer payload containing information about the dropped datasource. |
| `currentDataclass`    | `string`                   | The current dataclass associated with the target node.    |

#### Output

| **Output**  | **Description**                 |
|-------------|---------------------------------|
| `boolean`   | `true` if the dropped datasource belongs to the same dataclass; `false` otherwise. |




<!-- ################################################################################################################
###################################### use-enhanced-node/drop-indicator.tsx #########################################
#####################################################################################################################
-->

## use-enhanced-node/drop-indicator.tsx

<!-- ########### toggleDropIndicator ############ -->
### `toggleDropIndicator` Function

#### Purpose
A hook that toggles the visibility and styling of the drop indicator.

#### Signature

```tsx
toggleDropIndicator(
  targetdom?: OrNull<HTMLElement>,
  error?: boolean,
  root?: OrNull<HTMLElement>,
): void;
```

#### Input

| **Name**      | **Type**                     | **Description**                                           |
|---------------|------------------------------|-----------------------------------------------------------|
| `targetdom`   | `OrNull<HTMLElement>`        | The target DOM element where the drop indicator will be displayed. |
| `error`       | `boolean, optional`          | Indicates whether the drop indicator should represent an error state. |
| `root`        | `OrNull<HTMLElement>, optional` | The root DOM element to which the drop indicator should be appended. If not provided, it is appended to the document body. |

#### Output

| **Output**  | **Description**                 |
|-------------|---------------------------------|
| `void`      | This function does not return any value. |


#### Usage Example


<Tabs>
<TabItem value="Example 1">
Basic usage:

```tsx
import { toggleDropIndicator } from '@ws-ui/webform-editor';

const handleDrop = (e) => {
  const targetDom = /* ... */; // Get the target DOM element
  // highlight-next-line
  toggleDropIndicator(targetDom);
  // Additional handling for the drop event
};

// Attach the drop event handler to an HTML element
<div onDrop={handleDrop} onDragOver={(e) => e.preventDefault()}>
  {/* Your component content */}
</div>
```

</TabItem>

<TabItem value="Example 2">
With error state:

```tsx
import { toggleDropIndicator } from '@ws-ui/webform-editor';

const handleDropWithError = (e) => {
  const targetDom = /* ... */; // Get the target DOM element
  const isError = true; // Indicate an error state
  // highlight-next-line
  toggleDropIndicator(targetDom, isError);
  // Additional handling for the drop event
};

// Attach the drop event handler to an HTML element
<div onDrop={handleDropWithError} onDragOver={(e) => e.preventDefault()}>
  {/* Your component content */}
</div>
```

</TabItem>

<TabItem value="Example 3">
With root element:

```tsx
import { toggleDropIndicator } from '@ws-ui/webform-editor';

const handleDropWithRoot = (e) => {
  const targetDom = /* ... */; // Get the target DOM element
  const rootDom = /* ... */; // Specify the root DOM element
  // highlight-next-line
  toggleDropIndicator(targetDom, false, rootDom);
  // Additional handling for the drop event
};

// Attach the drop event handler to an HTML element
<div onDrop={handleDropWithRoot} onDragOver={(e) => e.preventDefault()}>
  {/* Your component content */}
</div>
```

</TabItem>

</Tabs>

<!-- ########### Constants ############ -->
### Constants

| **Constant**       | **Type**   | **Description**                                              |
|--------------------|------------|--------------------------------------------------------------|
| `INDICATOR_CLASS`  | `string`   | The CSS class for the drop indicator.                         |
| `INDICATOR_ERROR`  | `string`   | The CSS class for indicating an error state in the indicator. |




<!-- ################################################################################################################
########################################### use-enhanced-node/index.tsx #############################################
#####################################################################################################################
-->

## use-enhanced-node/index.tsx

<!-- ########### useEnhancedNode ############ -->
### `useEnhancedNode` Function

#### Purpose
A hook that enhances the functionality of a Craft.js node, providing features for handling data transfer, managing datasources, and styling components.

#### Signature
```tsx
useEnhancedNode<K>(
  collector?: (args: Node) => K,
  options?: {
    stopPropagation?: (data: IDataTransfer) => boolean;
    onDrop?: (e: any) => void;
  },
): {
    id: nodeId,
    store,
    connectors: { ...connectors, connect },
    ...collected,
    actions: {
      ...collected.actions,
    },
  };
```

#### Input

| **Name**  | **Type** | **Description**                 |
|-----------|----------|---------------------------------|
| `collector` (optional) | `(args: Node) => K` | A function to collect additional information from the node. |
| `options` (optional) | `{ stopPropagation?: (data: IDataTransfer) => boolean; onDrop?: (e: any) => void; }` | An object with optional properties ([`stopPropagation`](#stoppropagation) and [`onDrop`](#ondrop)) to customize the hook's behavior. |

#### Output

| **Output**  | **Description**                 |
|-------------|---------------------------------|
| `UseEnhancedNodeReturnType` | An object containing enhanced node information, connectors, and actions. |

:::info
The `useEnhancedNode` function returns an object with the following structure:

- **id**: The ID of the node.
- **store**: The store associated with the node.
- ***connectors***: Object containing connectors to interact with the Craft.js editor.
- **...collected**: Additional data collected by the collector function.
- **actions**: An object containing methods for manipulating node values, including `setProp`, `setStyle`, `setDatasource`, and `setIterator`.

:::

<!-- ########### Options ############ -->
#### Options

##### `stopPropagation`

| **Type**                | **Description**                                     |
|-------------------------|-----------------------------------------------------|
| `(data: IDataTransfer) => boolean`  | A callback function triggered to stop the propagation of data transfer.|

##### `onDrop`

| **Type**                | **Description**                             |
|-------------------------|-----------------------------------------------------|
| `(e: any) => void`  | A callback function triggered on the drop event.|


#### Usage Example


<Tabs>
<TabItem value="Example 1">
Basic usage:

```tsx
import { useEnhancedNode } from '@ws-ui/webform-editor';
import { useState, useEffect } from 'react';

const ExampleDelayedState = () => {
  // highlight-next-line
  const { actions, connectors, linkedNodes } = useEnhancedNode((node) => ({
    nodes: node.data.nodes,
    linkedNodes: node.data.linkedNodes,
    node,
  }));

  const [delayedState, setDelayedState] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      // Fetch your data, e.g., from an API
      const result = await fetch('https://api.example.com/data');
      const data = await result.json();

      setDelayedState(data);

      actions.setDatasourceValue({ key: 'yourDatasourceKey', value: data });
    };

    fetchData();
  }, [actions]);

  return (
    <div ref={connectors.connect}>
      {/* Your component content */}
      {delayedState && (
        <div>
          {JSON.stringify(delayedState)}
        </div>
      )}
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 2">
Handling drop events:

```tsx
import { useEnhancedNode } from '@ws-ui/webform-editor';

const DraggableComponent = () => {
  // highlight-next-line
  const { actions, connectors, linkedNodes } = useEnhancedNode((node) => ({
    nodes: node.data.nodes,
    linkedNodes: node.data.linkedNodes,
    node,
  }), {
    onDrop: (event) => {
      console.log('Dropped:', event);
    },
  });

  return (
    <div
      ref={connectors.connect}
      draggable
      onDragStart={(event) => {
        event.dataTransfer.setData('text', 'your data here');
      }}
    >
      {/* Your draggable component content */}
    </div>
  );
};
```

</TabItem>

</Tabs>






<!-- ################################################################################################################
######################################## use-sources/index.tsx ######################################################
#####################################################################################################################
-->

## use-sources/index.tsx

<!-- ########### useSources ############ -->
### `useSources` Function

#### Purpose
A hook that facilitates managing datasources and current elements associated with a web form. It provides methods for setting, fetching, and listening to changes in datasource values.

#### Signature

```tsx
useSources(options?: UseSourcesOptions): {
  sources: {
    datasource: datasources.DataSource;
    currentElement: datasources.DataSource;
  };
  actions: {
    setDatasourceValue: () => Promise<any>;
    setCurrentElementValue: () => Promise<any>;
    fetchDatasourceValue: () => Promise<any>;
    fetchCurrentElementValue: () => Promise<any>;
  };
};
```

#### Input

| **Name**  | **Type** | **Description**                 |
|-----------|----------|---------------------------------|
| `options` (optional) | `UseSourcesOptions` | An object allowing configuration of the hook behavior. Includes options such as [`datasourceChange`](#datasourcechange), [`currentElementChange`](#currentelementchange) and [`acceptIteratorSel`](#acceptiteratorsel). |


#### Output
| **Output**  | **Description**                 |
|-----------|---------------------------------|
| `UseSourcesReturnType`   | An object containing datasources, current elements, and methods for manipulating their values. |

:::info
The `useSources` function returns an object with the following structure:

- `sources`: An object containing `datasource` and `currentElement`, representing the current values of datasources and current elements.
- `actions`: An object containing methods for manipulating datasource values, including [`setDatasourceValue`](#actionssetdatasourcevalue), [`setCurrentElementValue`](#actionssetcurrentelementvalue), [`fetchDatasourceValue`](#actionsfetchdatasourcevalue), and [`fetchCurrentElementValue`](#actionsfetchcurrentelementvalue).
:::


<!-- ########### Options ############ -->
#### Options

##### `datasourceChange`

| **Type**                | **Description**                                     |
|-------------------------|-----------------------------------------------------|
| `() => void`  | A callback function triggered on datasource change.|

##### `currentElementChange`

| **Type**                | **Description**                                     |
|-------------------------|-----------------------------------------------------|
| `() => void`  | A callback function triggered on the change of the current element.        |

##### `acceptIteratorSel`

| **Type**                | **Description**                                     |
|-------------------------|-----------------------------------------------------|
| `boolean` \| `undefined`  | A boolean flag indicating whether to accept iterator selection. Defaults to `undefined`.|

<!-- ########### Methods ############ -->
#### Methods

##### `actions.setDatasourceValue`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| N/A | `Promise<any>` | Sets the value of the datasource. |

##### `actions.setCurrentElementValue`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| N/A | `Promise<any>` | Sets the value of the current element. |

##### `actions.fetchDatasourceValue`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| N/A | `Promise<any>` | Fetches the value of the datasource. |

##### `actions.fetchCurrentElementValue`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| N/A | `Promise<any>` | Fetches the value of the current element. |

#### Usage Example

```tsx
import { useSources } from "@ws-ui/webform-editor";

// code
```


<!-- ################################################################################################################
#################################################### events-selector.tsx ######################################################
#####################################################################################################################
-->

## events-selector.tsx


<!-- ########### selectEvents ############ -->
### `selectEvents` Function

#### Purpose
A hook that provides a selector function retrieving events based on the type, ID, and optional path.

#### Signature
```tsx
selectEvents(
  type: 'component' | 'datasource' | string,
  id: string,
  path?: string
): (state: AppState) => webforms.WEvent[];
```

#### Input

| **Parameter**  | **Type** | **Description**         |
|----------------|----------|-------------------------|
| `type`         | `component` \| `datasource` \| `string` | The type of the entity for which events are being retrieved. |
| `id`           | `string` | The ID of the component or datasource. |
| `path` (Optional)   | `string` \| `undefined` | The path to the webform tab. Defaults to the active tab in the state. |

#### Output

| **Output**  | **Description**                 |
|-----------|---------------------------------|
| `(state: AppState) => webforms.WEvent[]` | A selector function that, when called with the application state, returns an array of events associated with the specified entity. |

:::info
The `selectEvents` function uses `createSelector` from `@reduxjs/toolkit` to create a selector. It takes the complete Redux state (`AppState`) as an argument and returns an array of `webforms.WEvent[]`. This array contains events associated with the specified `type`, `id`, and `path`.
:::

#### Usage Example


<Tabs>
<TabItem value="Example 1">
Basic usage:

```tsx
import { selectEvents } from '@ws-ui/webform-editor';

const ExampleComponent1 = ({ entityId, entityType, tabPath }) => {
  // highlight-next-line
  const getEvents = useSelector(selectEvents(entityType, entityId, tabPath));
  const events = getEvents();

  return (
    <div>
      <h3>Events for {entityType} with ID {entityId}</h3>
      <ul>
        {events.map((event) => (
          <li key={event.id}>{event.name}</li>
        ))}
      </ul>
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 2">
Avoid re-renders with custom equality check:

```tsx
import { useSelector } from 'react-redux';
import { selectEvents } from '@ws-ui/webform-editor';

const ExampleComponent2 = ({ entityId, entityType, tabPath }) => {
  const events = useSelector(
    // highlight-next-line
    selectEvents(entityType, entityId, tabPath),
    // avoid re-renders when the old state & the new state are equal
    (left, right) => isEqual(left, right),
  );

  return (
    <div>
      <h3>Events for {entityType} with ID {entityId}</h3>
      <ul>
        {events.map((event) => (
          <li key={event.id}>{event.name}</li>
        ))}
      </ul>
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 3">
Using a default path:

```tsx
import { useSelector } from 'react-redux';
import { selectEvents } from '@ws-ui/webform-editor';

const ExampleComponent3 = ({ entityId, entityType }) => {
  // highlight-next-line
  const getEvents = useSelector(selectEvents(entityType, entityId));
  const events = getEvents();

  return (
    <div>
      <h3>Events for {entityType} with ID {entityId}</h3>
      <ul>
        {events.map((event) => (
          <li key={event.id}>{event.name}</li>
        ))}
      </ul>
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 4">
Using a specific path:

```tsx
import { useSelector } from 'react-redux';
import { selectEvents } from '@ws-ui/webform-editor';

const ExampleComponent4 = ({ entityId, entityType }) => {
  const customPath = "/custom-path"; // Replace with the desired path
  // highlight-next-line
  const getEvents = useSelector(selectEvents(entityType, entityId, customPath));
  const events = getEvents();

  return (
    <div>
      <h3>Events for {entityType} with ID {entityId}</h3>
      <ul>
        {events.map((event) => (
          <li key={event.id}>{event.name}</li>
        ))}
      </ul>
    </div>
  );
};
```

</TabItem>

</Tabs>




<!-- ################################################################################################################
#################################################### use-datasource-adapter.ts ######################################################
#####################################################################################################################
-->

## use-datasource-adapter.ts


<!-- ########### useDatasourceAdapter ############ -->
### `useDatasourceAdapter` Function

#### Purpose
A hook that provides methods and state information to interact with and manage a webform datasource.

#### Signature
```tsx
useDatasourceAdapter(datasourceId: string): {
  current: webforms.Datasource | undefined;
  query: {
    validateProperty: (propertyKey: string, value: any) => {
      ok: boolean;
      parsed: any;
      message: string;
      hasChange: boolean;
    };
  };
  actions: {
    editProperty: (property: string, value: any) => void;
    addEvent: (eventType: webforms.BaseEvent['type']) => void;
    editEvent: (eventId: string, property: string, value: any) => void;
    removeEvent: (eventId: string) => void;
    rename: (new_name: string) => Promise<boolean>;
    remove: () => void;
  };
};
```

#### Input

| **Parameter**  | **Type** | **Description**         |
|----------------|----------|-------------------------|
| `datasourceId` | `string` | The ID of the datasource. |

#### Output

| **Output**  | **Description**                 |
|-----------|---------------------------------|
| `DatasourceAdapterReturnType`   | An object containing the current datasource, query methods, and actions for managing the datasource. |

:::info
The `useDatasourceAdapter` function returns an object with the following structure:

- [`current`](#current): The current datasource object (either a `webforms.Datasource` or `undefined` if not found).
- `query`: An object containing a [`validateProperty`](#queryvalidateproperty) method for validating datasource properties.
- `actions`: An object containing methods to perform actions on the datasource, including [`editProperty`](#actionseditproperty), [`addEvent`](#actionsaddevent), [`editEvent`](#actionseditevent), [`removeEvent`](#actionsremoveevent), [`rename`](#actionsrename), and [`remove`](#actionsremove).
:::

#### Properties

##### `current`

| **Type** | **Description** |
|----------|-----------------|
| `webforms.Datasource` \| `undefined` | The current datasource object. |


#### Methods

##### `query.validateProperty`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `propertyKey` (string), `value` (any) | `{ ok: boolean, parsed: any, message: string, hasChange: boolean }` | Validates a datasource property and returns an object with validation information. |

##### `actions.editProperty`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `property` (string), `value` (any) | N/A | Edits a datasource property with the specified value. |

##### `actions.addEvent`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `eventType` (webforms.BaseEvent['type']) | N/A | Adds a new event of the specified type to the datasource. |

##### `actions.editEvent`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `eventId` (string), `property` (string), `value` (any) | `boolean` | Edits an existing event with the specified property and value. Returns `true` if the edit is successful, otherwise `false`. |

##### `actions.removeEvent`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `eventId` (string) | N/A | Removes an event with the specified ID from the datasource. |

##### `actions.rename`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `new_name` (string) | `Promise<boolean>` | Renames the datasource to the specified new name. Returns a promise that resolves to `true` if the rename is confirmed, otherwise `false`. |

##### `actions.remove`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| N/A | N/A | Removes the current datasource. |


#### Usage Example

<Tabs>
<TabItem value="Example 1">
Basic usage:

```tsx
import { useDatasourceAdapter } from "@ws-ui/webform-editor";

const BasicExample = () => {
  // highlight-next-line
  const { current, query, actions } = useDatasourceAdapter("someDatasourceId");

  return (
    <div>
      <p>Current Datasource Name: {current?.name}</p>
      <p>Current Datasource Type: {current?.type}</p>

      <p>Validation Result for Name: {JSON.stringify(query.validateProperty("name", "New Datasource Name"))}</p>

      <button onClick={() => actions.editProperty("name", "New Datasource Name")}>
        Edit Datasource Name
      </button>
    </div>
  );
}
```

</TabItem>

<TabItem value="Example 2">
Adding an event:

```tsx
import { useDatasourceAdapter } from "@ws-ui/webform-editor";

const AddEventExample = (props: { datasourceId: string }) => {
  // highlight-next-line
  const { current, actions } = useDatasourceAdapter(props.datasourceId);

  const addMethodEvent = () => {
    // highlight-next-line
    actions.addEvent('method');
  };

  return (
    <div>
      <p>Current Datasource Name: {current?.name}</p>

      {/* Adding an Event Example */}
      <button onClick={addMethodEvent}>Add Method Event</button>
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 3">
Editing an event:

```tsx
import { useDatasourceAdapter } from "@ws-ui/webform-editor";

const EditEventExample = (props: { datasourceId: string }) => {
  // highlight-next-line
  const { current, actions } = useDatasourceAdapter(props.datasourceId);

  const editEvent = (eventId, property, value) => {
    // highlight-next-line
    actions.editEvent(eventId, property, value);
  };

  return (
    <div>
      <p>Current Datasource Name: {current?.name}</p>

      {/* Editing an Event Example */}
      <button onClick={() =>
          editEvent(current?.events[0]?.id, 'method', 'newMethod')
        }>
        Edit Event Method
      </button>
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 4">
Removing an event:

```tsx
import { useDatasourceAdapter } from "@ws-ui/webform-editor";

const RemoveEventExample = (props: { datasourceId: string }) => {
  // highlight-next-line
  const { current, actions } = useDatasourceAdapter(props.datasourceId);

  const removeEvent = (eventId) => {
    // highlight-next-line
    actions.removeEvent(eventId);
  };

  return (
    <div>
      <p>Current Datasource Name: {current?.name}</p>

      {/* Removing an Event Example */}
      <button onClick={() => removeEvent(current?.events[0]?.id)}>
        Remove Event
      </button>
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 5">
Renaming the datasource:

```tsx
import { useDatasourceAdapter } from "@ws-ui/webform-editor";

const RenameDatasourceExample = (props: { datasourceId: string }) => {
  // highlight-next-line
  const { actions } = useDatasourceAdapter(props.datasourceId);

  const renameDatasource = (newName) => {
    // highlight-next-line
    actions.rename(newName);
  };

  return (
    <div>
      {/* Renaming the Datasource Example */}
      <button onClick={() => renameDatasource("New Datasource Name")}>
        Rename Datasource
      </button>
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 6">
Removing the datasource:

```tsx
import { useDatasourceAdapter } from "@ws-ui/webform-editor";

const RemoveDatasourceExample = (props: { datasourceId: string }) => {
  // highlight-next-line
  const { actions } = useDatasourceAdapter(props.datasourceId);

  const removeDatasource = () => {
    // highlight-next-line
    actions.remove();
  };

  return (
    <div>
      {/* Removing the Datasource Example */}
      <button onClick={removeDatasource}>Remove Datasource</button>
    </div>
  );
};
```

</TabItem>

</Tabs>





<!-- ################################################################################################################
#################################################### use-datasources-subscription.ts ######################################################
#####################################################################################################################
-->

## use-datasources-subscription.ts

<!-- ########### useDatasourceSub ############ -->
### `useDatasourceSub` Function

#### Purpose
A hook that subscribes to changes in datasources and performs replacements in the webform based on specified actions.

#### Signature
```tsx
useDatasourceSub(): void;
```

#### Input (N/A)

#### Output (N/A)

#### Usage Example

```tsx
import useDatasourceSub from "@ws-ui/webform-editor"

const ExampleComponent = () => {
  // highlight-next-line
  useDatasourceSub();
};
```




<!-- ################################################################################################################
#################################################### use-delayed-state.ts ######################################################
#####################################################################################################################
-->

## use-delayed-state.ts

<!-- ########### useDelayedState ############ -->
### `useDelayedState` Function

#### Purpose
A hook that manages state with a delayed update using `setTimeout`.

#### Signature
```tsx
useDelayedState<S>(
  initialState: S | (() => S),
  delay: number = 0,
): [S, Dispatch<SetStateAction<S>>];
```

#### Input

| **Parameter**  | **Type**                           | **Description**                                         |
|----------------|------------------------------------|---------------------------------------------------------|
| `initialState` | `S` \| `(() => S)`                 | The initial state value or a function returning the initial state. |
| `delay` (Optional)        | `number`                |  The delay (in milliseconds) before updating the state (default is 0). |

#### Output

| **Output**  | **Description**                                         |
|-----------|---------------------------------------------------------|
| `[S, Dispatch<SetStateAction<S>>]` | A tuple containing the current state and a function to update the state with a delayed action. |

:::info
The `useDelayedState` function returns an array with two elements:

- `state`: The current state value.
- `updateState`: A function that can be used to update the state with a delay. It has the same signature as the `setState` function from React.
:::

#### Usage Examples

```tsx
import React, { useEffect } from 'react';
import { useDelayedState } from "@ws-ui/webform-editor";

const ExampleDelayedState = () => {
  // Initialize state with a delay of 1000 milliseconds
  // highlight-next-line
  const [loaded, setLoaded] = useDelayedState(false, 1000);

  // Simulate an effect that triggers a state update after some time
  useEffect(() => {
    // Simulating a network request or time-consuming operation
    const fetchData = async () => {
      await new Promise((resolve) => setTimeout(resolve, 2000));
      // Update the state after the operation is complete
      // highlight-next-line
      setLoaded(true);
    };

    // Call the fetchData function
    fetchData();
  }, [setLoaded]);

  // The rest of your component logic...
  // highlight-next-line
  if (loaded) {
    // Render content after the delay and data are loaded
    return <div>Data Loaded!</div>;
  } else {
    // Render loading state or placeholder
    return <div>Loading...</div>;
  }
};
```






<!-- ################################################################################################################
#################################################### use-ds-autosuggest.ts ######################################################
#####################################################################################################################
-->

## use-ds-autosuggest.ts


<!-- ########### useDsAutosuggest ############ -->
### `useDsAutosuggest` Function

#### Purpose
A hook that facilitates the implementation of autosuggest functionality, enabling the search and selection of datasources, fields, and attributes within a webform editor.

#### Signature
```tsx
useDsAutosuggest({
  exclude?: 'private' | 'shared';
  parentNode?: IUseIterableParentNodeReturnType | null;
  source?: ISplitDatasource;
  initialNamespace?: string;
  onSelectedItemChange: (changes: UseComboboxStateChange<Item>) => void;
  filter?: TDatasourcesFilter;
  notIn?: TDatasourcesNotIn;
  maxDepth?: number;
  onSourceChange?: Function;
}): {
  ...comboBoxProps,
  items: Item[];
  getInputProps: (
    options?: UseComboboxGetInputPropsOptions,
    otherOptions?: GetPropsCommonOptions
  ) => { [key: string]: any };
};
```

#### Input

| **Parameter**            | **Type**                                   | **Description**                                                                                                                                                                          |
|--------------------------|--------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `exclude` (Optional)     | `private` \| `shared`                   | Specifies whether to exclude private or shared datasources.                                                                                                                              |
| `parentNode` (Optional)  | `IUseIterableParentNodeReturnType` \| `null` | Represents the parent node of the iterable, used to determine the iterator.                                                                                                             |
| `source` (Optional)      | `ISplitDatasource`                         | Used in the datatable component columns.                                                                                                                                                 |
| `initialNamespace`       | `string` \| `undefined`                      | Specifies the initial namespace.                                                                                                                                                         |
| `onSelectedItemChange`   | `(changes: UseComboboxStateChange<Item>) => void` | Callback function triggered on selected item change.                                                                                                                                   |
| `filter` (Optional)      | `TDatasourcesFilter`                       | Specifies additional filtering criteria for datasources.                                                                                                                                |
| `notIn` (Optional)       | `TDatasourcesNotIn`                        | Specifies datasources that should not be included.                                                                                                                                      |
| `maxDepth` (Optional)    | `number`                                   | Limits the depth of the search hierarchy.                                                                                                                                               |
| `onSourceChange` (Optional) | `Function`                                 | Callback function triggered on source change.                                                                                                                                           |

#### Output

| **Output**   | **Description**  |
|------------------------|--------------------|
| `UseComboboxState<Item>` | An object containing the state and functions provided by the `useCombobox` hook, along with additional properties for handling autosuggest functionality.|

:::info
The `useDsAutosuggest` function returns an object with the following properties:

- `...comboBoxProps`: This includes the state properties and functions provided by the `useCombobox` hook. It allows you to manage the state of the autosuggest component.

- `items: Item[]`: An array of items representing the suggestions to be displayed in the autosuggest dropdown. Each item has properties such as `name`, `type`, `namespace`, and `index`.

- `getInputProps: (options?: UseComboboxGetInputPropsOptions, otherOptions?: GetPropsCommonOptions) => InputProps`: A function that returns props for the input element. These props are necessary for integrating the autosuggest functionality into an input component. The actual type of `InputProps` may vary based on the `downshift` library or specific types used in the implementation.
:::


#### Usage Example

<Tabs>
<TabItem value="Example 1">
Basic usage:

```tsx
import { useDsAutosuggest } from "@ws-ui/webform-editor";

// highlight-next-line
const {getInputProps, getMenuProps, getItemProps, isOpen, items } = useDsAutosuggest({
  onSelectedItemChange: ({ selectedItem: selected }) => {
    if (selected) {
      console.log(`Selected Item: ${selected.name} (${selected.namespace})`);
    }
  },
});

return (
  <div>
    <input {...getInputProps()} />
    <ul {...getMenuProps()}>
      {isOpen &&
        items.map((item, index) => (
          <li key={index} {...getItemProps({ item })}>
            {item.name} ({item.namespace})
          </li>
        ))}
    </ul>
  </div>
);
```

</TabItem>

<TabItem value="Example 2">
Integration with component:

```tsx
import { useDsAutosuggest } from "@ws-ui/webform-editor";

// highlight-next-line
const { getInputProps, getMenuProps, getItemProps, isOpen, items } = useDsAutosuggest({
  exclude: 'private',
  initialNamespace: 'exampleNamespace',
  onSelectedItemChange: ({ selectedItem: selected }) => {
    if (selected) {
      console.log(`Selected Item: ${selected.name} (${selected.namespace})`);
    }
  },
});

return (
  <div>
    <ReturnValueField data={data} exclude={exclude} />
    <input {...getInputProps()} />
    <ul {...getMenuProps()}>
      {isOpen &&
        items.map((item, index) => (
          <li key={index} {...getItemProps({ item })}>
            {item.name} ({item.namespace})
          </li>
        ))}
    </ul>
  </div>
);
```

</TabItem>

<TabItem value="Example 3">
Custom event handling:

```tsx
import { useDsAutosuggest } from "@ws-ui/webform-editor";

// highlight-next-line
const { getInputProps, getMenuProps, getItemProps, isOpen, items } = useDsAutosuggest({
  onSelectedItemChange: ({ selectedItem: selected }) => {
    if (selected) {
      console.log(`Custom Event Handling - Selected Item: ${selected.name}`);
    }
  },
});

return (
  <div>
    <input {...getInputProps({
        onKeyDown: (e) => {
          if (e.key === 'Enter') {
            console.log('Enter key pressed!');
          }
        },
      })}
    />
    <ul {...getMenuProps()}>
      {isOpen &&
        items.map((item, index) => (
          <li key={index} {...getItemProps({ item })}>
            {item.name}
          </li>
        ))}
    </ul>
  </div>
);
```

</TabItem>

<TabItem value="Example 4">
Advanced styling and configuration:

```tsx
import { useDsAutosuggest } from "@ws-ui/webform-editor";

// highlight-next-line
const {getInputProps, getMenuProps, getItemProps, isOpen, items, getComboboxProps } = useDsAutosuggest({
  exclude: 'shared',
  initialNamespace: 'customNamespace',
  onSelectedItemChange: ({ selectedItem: selected }) => {
    if (selected) {
      console.log(`Selected Item: ${selected.name} (${selected.namespace})`);
    }
  },
});

return (
  <div {...getComboboxProps({ className: 'custom-autosuggest' })}>
    <input {...getInputProps({ placeholder: 'Search...' })} />
    <ul {...getMenuProps({ className: 'custom-menu' })}>
      {isOpen &&
        items.map((item, index) => (
          <li key={index} {...getItemProps({ item, className: 'custom-item' })}>
            {item.name} ({item.namespace})
          </li>
        ))}
    </ul>
  </div>
);
```

</TabItem>

</Tabs>


<!-- ########### getDataclassByPath ############ -->
### `getDataclassByPath` Helper Function

#### Purpose
A helper function that retrieves a detailed data class based on the provided path and catalog.

#### Signature
```tsx
getDataclassByPath(
  path: string,
  catalog: datasources.IEnhancedCatalog
): datasources.IDetailedDataClass | undefined;
```

#### Input

| **Parameter** | **Type**                           | **Description**                                         |
|---------------|------------------------------------|---------------------------------------------------------|
| `path`        | `string`                           | The path to the data class.                             |
| `catalog`     | `datasources.IEnhancedCatalog`     | The catalog containing data classes.                    |

#### Output

| **Output**      | **Description**                                         |
|---------------|---------------------------------------------------------|
| `datasources.IDetailedDataClass` \| `undefined` | The detailed data class or `undefined` if not found.     |


<!-- ########### getType ############ -->
### `getType` Helper Function

#### Purpose
A helper function that determines the type of a datasource attribute.

#### Signature
```tsx
getType(attribute: datasources.IAttribute): datasources.TDatasourceType;
```

#### Input

| **Parameter** | **Type**                           | **Description**                                         |
|---------------|------------------------------------|---------------------------------------------------------|
| `attribute`   | `datasources.IAttribute`           | The datasource attribute.                               |

#### Output

| **Output**      | **Description**                                         |
|---------------|---------------------------------------------------------|
| `datasources.TDatasourceType` | The type of the datasource attribute.  |





<!-- ################################################################################################################
#################################################### use-editor-helpers.ts ######################################################
#####################################################################################################################
-->

## use-editor-helpers.ts

A module providing helper functions for interacting with the Craft.js editor state.

<!-- ########### selectReadOnly ############ -->
### `selectReadOnly` Editor Collector

#### Purpose
A function that collects and returns the read-only state information from the Craft.js editor.

#### Signature
```tsx
selectReadOnly: EditorCollector<{ enabled: boolean }> = (
  state,
) => ({ enabled: state.options.enabled });
```

#### Input

| **Parameter** | **Type**                           | **Description**                                         |
|---------------|------------------------------------|---------------------------------------------------------|
| `state`       | `CraftEditorState`                  | The current state of the Craft.js editor.                |

#### Output

| **Output**      | **Description**                                         |
|---------------|---------------------------------------------------------|
| `{ enabled: boolean }` | An object containing the `enabled` property indicating whether the editor is in read-only mode.     |



<!-- ########### selectResolver ############ -->
### `selectResolver` Editor Collector

#### Purpose
A function that collects and returns the resolver information from the Craft.js editor.

#### Signature
```tsx
selectResolver: EditorCollector<{ resolver: any }> = (state) => ({
  resolver: state.options.resolver,
});
```

#### Input

| **Parameter** | **Type**                           | **Description**                                         |
|---------------|------------------------------------|---------------------------------------------------------|
| `state`       | `CraftEditorState`                  | The current state of the Craft.js editor.                |

#### Output

| **Output**      | **Description**                                         |
|---------------|---------------------------------------------------------|
| `{ resolver: any }` | An object containing the `resolver` property with the resolver information from the editor options.     |


<!-- ########### selectNodeId ############ -->
### `selectNodeId` Function

#### Purpose
A function that takes a Craft.js Node and returns an object containing the `nodeId` property.

#### Signature
```tsx
selectNodeId = (node: Node) => ({
  nodeId: string;
});

```

#### Input

| **Parameter** | **Type**                           | **Description**                                         |
|---------------|------------------------------------|---------------------------------------------------------|
| `node`        | `Node`                             | A Craft.js Node instance.                                |

#### Output

| **Output**      | **Description**                                         |
|---------------|---------------------------------------------------------|
| `{ nodeId: string }` | An object containing the `nodeId` property with the ID of the provided Craft.js Node.     |

#### Usage Example

```tsx
import { selectNodeId } from "@ws-ui/webform-editor";

// code
```

<!-- ################################################################################################################
#################################################### use-enhanced-editor.ts ######################################################
#####################################################################################################################
-->

## use-enhanced-editor.ts

<!-- ########### useEnhancedEditor ############ -->
### `useEnhancedEditor` Function

#### Purpose
A hook that provides methods and state information associated with the enhanced editor.

#### Signature

<Tabs>
<TabItem value="Signature 1">

```tsx
useEnhancedEditor(): useEditorReturnType;
```

</TabItem>

<TabItem value="Signature 2">

```tsx
useEnhancedEditor<S>(collect: EditorCollector<S>): useEditorReturnType<S>;
```

</TabItem>

<TabItem value="Signature 3">

```tsx
useEnhancedEditor<S>(collect?: any): useEditorReturnType<S>;
```

</TabItem>

</Tabs>

#### Input

| **Parameter**  | **Type** | **Description**         |
|----------------|----------|-------------------------|
| `collect` (Optional)     | `EditorCollector<S>` | A function that collects relevant state information from the editor state. The component will re-render when the values returned by this function change. |

#### Output

| **Output**  | **Description**                 |
|-----------|---------------------------------|
| `useEditorReturnType`   | An object containing properties and methods related to the Craft.js editor. |

:::info
The `useEnhancedEditor` function returns an object with properties and methods from the `useEditor` hook. Additionally, it extends the `actions` object with a `delete` method that allows for deleting nodes, with special handling for nodes with roles such as 'tab' and 'grid-area'.
:::

#### Usage Examples

<Tabs>
<TabItem value="Example 1">
Basic usage:

```tsx
import { useEnhancedEditor } from "@ws-ui/webform-editor";

const BasicUsageExample = () => {
  // highlight-next-line
  const { isActive, enabled, canvas } = useEnhancedEditor();

  // Your component logic based on the editor state
  return (
    <div>
      <p>Is Active: {isActive ? 'Yes' : 'No'}</p>
      <p>Editor Enabled: {enabled ? 'Yes' : 'No'}</p>
      <p>Canvas Element: {canvas}</p>

      {/* Additional logic and components based on the editor state */}
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 2">
Basic usage with collector:

```tsx
import { useEnhancedEditor } from "@ws-ui/webform-editor";

const CollectorUsageExample = () => {
  const collect = (state, query) => ({
    enabled: state.options.enabled,
    isActive: query.getEvent('selected').some(),
  });
  // highlight-next-line
  const { isActive, enabled, actions } = useEnhancedEditor(collect);

  // Your component logic based on the collected data
  return (
    <div>
      <p>Is Active: {isActive ? 'Yes' : 'No'}</p>
      <p>Editor Enabled: {enabled ? 'Yes' : 'No'}</p>

      {/* Additional logic and components based on the collected data */}
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 3">
Usage with a custom collector function:

```tsx
import { useEnhancedEditor } from "@ws-ui/webform-editor";

const CustomUsageExample = ({ id }) => {
  const { hidden, selected, hovered, topLevel } =
    useEnhancedEditor((state, query) => {
      const node = state.nodes[id];
      const nodeActions = query.node(id);

      return {
        hidden: node?.data.hidden,
        selected: state.events.selected.has(id),
        topLevel: node ? nodeActions.isTopLevelCanvas() : false,
        hovered: state.events.hovered.has(id),
      };
    });

  // Your component logic based on the useEnhancedEditor results
  return (
    <div>
      <p>Is Hidden: {hidden ? 'Yes' : 'No'}</p>
      <p>Is Selected: {selected ? 'Yes' : 'No'}</p>
      <p>Is Top Level: {topLevel ? 'Yes' : 'No'}</p>
      <p>Is Hovered: {hovered ? 'Yes' : 'No'}</p>

      {/* Additional logic and components based on the useEnhancedEditor results */}
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 4">
Deleting a node by ID:

```tsx
import { useEnhancedEditor } from "@ws-ui/webform-editor";

const Example = () => {
  // highlight-next-line
  const { actions } = useEnhancedEditor();

  const deleteNode = (nodeId) => {
    actions.delete(nodeId);
  };

  return (
    <button onClick={() => deleteNode('someNodeId')}>
      Delete Node
    </button>
  );
}
```

</TabItem>

</Tabs>






<!-- ################################################################################################################
#################################################### use-events-adapter.ts ######################################################
#####################################################################################################################
-->

## use-events-adapter.ts


<!-- ########### useEventsAdapter ############ -->
### `useEventsAdapter` Function

#### Purpose
A hook that provides methods and state information to interact with and manage events for a selected element (either a component or a datasource) in a web form.


#### Signature
```tsx
useEventsAdapter(type: string, id: string): {
  list: webforms.WEvent[];
  supported: webforms.EventMeta[];
  query: {
    event: (eventId: string) => webforms.WEvent | undefined;
  };
  actions: {
    event: {
      reorder: (leftIndex: number, rightIndex: number) => webforms.WEvent[];
      add: (type: webforms.BaseEvent['type'], eventNames: string[]) => boolean;
      edit: (eventId: string, payload: Partial<webforms.WEvent>) => void;
      delete: (eventId: string) => void;
      toggleDisabled: (eventId: string) => void;
    };
    params: {
      add: (eventId: string, defaultType?: string) => void;
      transform: (eventId: string, payload: { params: webforms.MethodParam[]; variadicType: string; }) => void;
      edit: (eventId: string, paramId: string, payload: Partial<webforms.MethodParam>) => void;
      delete: (eventId: string, paramId: string) => void;
      toggleHardCoded: (eventId: string, paramId: string) => void;
    };
    queries: {
      add: (eventId: string) => void;
      edit: (eventId: string, payload: Partial<webforms.QueryString>) => void;
      editParam: (eventId: string, paramId: string, payload: Partial<webforms.QueryParam>) => void;
      delete: (eventId: string, paramId: string) => void;
      toggleHardCoded: (eventId: string, paramId: string) => void;
    };
    returns: {};
  };
};
```

#### Input

| **Parameter**  | **Type** | **Description**         |
|----------------|----------|-------------------------|
| `type` | `string` | The type of the selected element (`component` or `datasource`). |
| `id` | `string` | The ID of the selected element. |

#### Output

| **Output**  | **Description**                 |
|-----------|---------------------------------|
| `EventsAdapterReturnType`   | An object containing the list of configured events, supported events, query methods, and actions to manipulate events for the selected element. |

:::info
The `useEventsAdapter` function returns an object with properties [`list`](#list) and [`supported`](#supported), and methods:

- [`query.event`](#queryevent)
- `actions.event` with methods [`reorder`](#actionseventreorder), [`add`](#actionseventadd), [`edit`](#actionseventadd), [`delete`](#actionseventdelete), and [`toggleDisabled`](#actionseventtoggledisabled).
- `actions.params` with methods [`add`](#actionsparamsadd), [`transform`](#actionsparamstransform), [`edit`](#actionsparamsedit), [`delete`](#actionsparamsdelete), and [`toggleHardCoded`](#actionsparamstogglehardcoded).
- `actions.queries` with methods [`add`](#actionsqueriesadd), [`edit`](#actionsqueriesedit), [`editParam`](#actionsquerieseditparam), [`delete`](#actionsqueriesdelete), and [`toggleHardCoded`](#actionsqueriestogglehardcoded).

:::

<!-- ########### Properties ############ -->
#### Properties

##### `list`

| **Type** | **Description** |
|----------|-----------------|
| `webforms.WEvent[]` | List of configured events for the selected element. |

##### `supported`

| **Type** | **Description** |
|----------|-----------------|
| `webforms.EventMeta[]` | List of supported events for the selected element. |


<!-- ########### Methods ############ -->
#### Methods

##### `query.event`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `eventId` (string) | `webforms.WEvent` \| `undefined` | Returns the configured event in the selected element if found, `undefined` otherwise. |

##### `actions.event.reorder`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `leftIndex` (number), `rightIndex` (number) | `webforms.WEvent[]` | Reorders the list of events for the selected element. |

##### `actions.event.add`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `type` (webforms.BaseEvent['type']), `eventNames` (string[]) | `boolean` | Adds a new event based on the type using a default config. Returns `true` if the event has been added successfully. |

##### `actions.event.edit`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `eventId` (string), `payload` (Partial<webforms.WEvent\>) | N/A | Assigns the new payload to the event. |

##### `actions.event.delete`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `eventId` (string) | N/A | Removes an event from the list. |

##### `actions.event.toggleDisabled`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `eventId` (string) | N/A | Toggles the disabled property for the specified event. |

##### `actions.params.add`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `eventId` (string), `defaultType` (string \| undefined) | N/A | Adds a new param to an event with a default config. |

##### `actions.params.transform`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `eventId` (string), `payload` ({ params: webforms.MethodParam[], variadicType: string }) | N/A | Transforms params if it has variadic params "...". |

##### `actions.params.edit`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `eventId` (string), `paramId` (string), `payload` (Partial<webforms.MethodParam\>) | N/A | Edits the content of an event param. |

##### `actions.params.delete`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `eventId` (string), `paramId` (string) | N/A | Deletes the param from the target event. |

##### `actions.params.toggleHardCoded`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `eventId` (string), `paramId` (string) | N/A | Toggles the hardcoded property for the param. |

##### `actions.queries.add`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `eventId` (string) | N/A | Adds a new query param into the query string of an event. |

##### `actions.queries.edit`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `eventId` (string), `payload` (Partial<webforms.QueryString\>) | N/A | Edits a query for a given event. |

##### `actions.queries.editParam`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `eventId` (string), `paramId` (string), `payload` (Partial<webforms.QueryParam\>) | N/A | Edits a query param for a given event. |

##### `actions.queries.delete`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `eventId` (string), `paramId` (string) | N/A | Deletes the query param for a given event. |

##### `actions.queries.toggleHardCoded`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `eventId` (string), `paramId` (string) | N/A | Toggles the hardcoded property for a query param of a given event. |

##### `actions.returns`

No specific actions provided for `returns` property.


<!-- ########### examples ############ -->
#### Usage Example

<Tabs>

<TabItem value="Exp 1">
Basic usage:

```tsx
import { useEventsAdapter } from "@ws-ui/webform-editor";

const BasicExample = () => {
  // highlight-next-line
  const { list, supported, query, actions } = useEventsAdapter("component", "someComponentId");

  return (
    <div>
      <p>List of Configured Events: {JSON.stringify(list)}</p>
      <p>Supported Events: {JSON.stringify(supported)}</p>

      <p>Query for Event with ID "eventId": {JSON.stringify(query.event("eventId"))}</p>

      <button onClick={() => actions.event.reorder(1, 3)}>
        Reorder Events
      </button>
    </div>
  );
}
```

</TabItem>

<TabItem value="Exp 2">
Adding an event:

```tsx
import { useEventsAdapter } from "@ws-ui/webform-editor";

const AddEventExample = (props: { type: string, id: string }) => {
  // highlight-next-line
  const { actions } = useEventsAdapter(props.type, props.id);

  const addEvent = () => {
    // highlight-next-line
    actions.event.add('simple-action', ['onclick']);
  };

  return (
    <div>
      <button onClick={addEvent}>Add Event</button>
    </div>
  );
};
```

</TabItem>

<TabItem value="Exp 3">
Editing an event:

```tsx
import { useEventsAdapter } from "@ws-ui/webform-editor";

const EditEventExample = (props: { type: string, id: string }) => {
  // highlight-next-line
  const { actions } = useEventsAdapter(props.type, props.id);

  const editEvent = (eventId, payload) => {
    // highlight-next-line
    actions.event.edit(eventId, payload);
  };

  return (
    <div>
      <button onClick={() =>
        editEvent('eventId', { action: 'newAction' })
      }>
        Edit Event
      </button>
    </div>
  );
};
```

</TabItem>

<TabItem value="Exp 4">
Removing an event:

```tsx
import { useEventsAdapter } from "@ws-ui/webform-editor";

const RemoveEventExample = (props: { type: string, id: string }) => {
  // highlight-next-line
  const { actions } = useEventsAdapter(props.type, props.id);

  const removeEvent = (eventId) => {
    // highlight-next-line
    actions.event.delete(eventId);
  };

  return (
    <div>
      <button onClick={() => removeEvent('eventId')}>
        Remove Event
      </button>
    </div>
  );
};
```

</TabItem>

<TabItem value="Exp 5">
Adding a parameter to an event:

```tsx
import { useEventsAdapter } from "@ws-ui/webform-editor";

const AddParamExample = (props: { type: string, id: string }) => {
  // highlight-next-line
  const { actions } = useEventsAdapter(props.type, props.id);

  const addParam = () => {
    // highlight-next-line
    actions.params.add('eventId', 'defaultType');
  };

  return (
    <div>
      <button onClick={addParam}>Add Param</button>
    </div>
  );
};
```

</TabItem>

<TabItem value="Exp 6">
Editing a parameter of an event:

```tsx
import { useEventsAdapter } from "@ws-ui/webform-editor";

const EditParamExample = (props: { type: string, id: string }) => {
  // highlight-next-line
  const { actions } = useEventsAdapter(props.type, props.id);

  const editParam = (eventId, paramId, payload) => {
    // highlight-next-line
    actions.params.edit(eventId, paramId, payload);
  };

  return (
    <div>
      <button onClick={() =>
        editParam('eventId', 'paramId', { type: 'newType' })
      }>
        Edit Param
      </button>
    </div>
  );
};
```

</TabItem>

<TabItem value="Exp 7">
Deleting a parameter from an event:

```tsx
import { useEventsAdapter } from "@ws-ui/webform-editor";

const DeleteParamExample = (props: { type: string, id: string }) => {
  // highlight-next-line
  const { actions } = useEventsAdapter(props.type, props.id);

  const deleteParam = (eventId, paramId) => {
    // highlight-next-line
    actions.params.delete(eventId, paramId);
  };

  return (
    <div>
      <button onClick={() => deleteParam('eventId', 'paramId')}>
        Delete Param
      </button>
    </div>
  );
};
```

</TabItem>

<TabItem value="Exp 8">
Adding a query to an event:

```tsx
import { useEventsAdapter } from "@ws-ui/webform-editor";

const AddQueryExample = (props: { type: string, id: string }) => {
  // highlight-next-line
  const { actions } = useEventsAdapter(props.type, props.id);

  const addQuery = () => {
    // highlight-next-line
    actions.queries.add('eventId');
  };

  return (
    <div>
      <button onClick={addQuery}>Add Query</button>
    </div>
  );
};
```

</TabItem>

<TabItem value="Exp 9">
Editing a query of an event:

```tsx
import { useEventsAdapter } from "@ws-ui/webform-editor";

const EditQueryExample = (props: { type: string, id: string }) => {
  // highlight-next-line
  const { actions } = useEventsAdapter(props.type, props.id);

  const editQuery = (eventId, payload) => {
    // highlight-next-line
    actions.queries.edit(eventId, payload);
  };

  return (
    <div>
      <button onClick={() =>
        editQuery('eventId', { datasource: 'newDatasource' })
      }>
        Edit Query
      </button>
    </div>
  );
};
```

</TabItem>

<TabItem value="Exp 10">
Deleting a query from an event:

```tsx
import { useEventsAdapter } from "@ws-ui/webform-editor";

const DeleteQueryExample = (props: { type: string, id: string }) => {
  // highlight-next-line
  const { actions } = useEventsAdapter(props.type, props.id);

  const deleteQuery = (eventId, paramId) => {
    // highlight-next-line
    actions.queries.delete(eventId, paramId);
  };

  return (
    <div>
      <button onClick={() => deleteQuery('eventId', 'paramId')}>
        Delete Query
      </button>
    </div>
  );
};
```

</TabItem>

<TabItem value="Exp 11">
Toggling hardcoded property for a parameter:

```tsx
import { useEventsAdapter } from "@ws-ui/webform-editor";

const ToggleHardCodedExample = (props: { type: string, id: string }) => {
  // highlight-next-line
  const { actions } = useEventsAdapter(props.type, props.id);

  const toggleHardCoded = (eventId, paramId) => {
    // highlight-next-line
    actions.params.toggleHardCoded(eventId, paramId);
  };

  return (
    <div>
      <button onClick={() => toggleHardCoded('eventId', 'paramId')}>
        Toggle Hardcoded
      </button>
    </div>
  );
};
```

</TabItem>

</Tabs>






<!-- ################################################################################################################
#################################################### use-forwarded-ref.ts ######################################################
#####################################################################################################################
-->

## use-forwarded-ref.ts


<!-- ########### useForwardedRef ############ -->
### `useForwardedRef` Function

#### Purpose

A hook that simplifies the management of forwarded refs in React components by creating an inner ref usable within the component. It guarantees proper updating of the outer forwarded ref whenever changes occur in the inner ref.

#### Signature

```tsx
useForwardedRef<T>(ref: ForwardedRef<T>): React.MutableRefObject<T>;
```

#### Input

| **Parameter**  | **Type** | **Description**         |
|----------------|----------|-------------------------|
| `ref` | `React.ForwardedRef<T>` | The forwarded ref provided by the parent component. |

#### Output

| **Output**  | **Description**                 |
|-----------|---------------------------------|
| `React.MutableRefObject<T>`   | An inner ref object that corresponds to the inner ref created using `useRef<T>(null)` and is updated based on the provided `ForwardedRef<T>`. The inner ref is managed internally to ensure proper forwarding of the ref. |

#### Usage Example

<Tabs>
<TabItem value="Example 1">
Basic usage:

```tsx
import useRef from 'react';
import { CTextfield, useForwardedRef } from "@ws-ui/webform-editor";

const MyComponent = () => {
  const inputRef = useRef<HTMLInputElement | null>(null);
  // highlight-next-line
  const forwardedRef = useForwardedRef(inputRef);

  return (
    <div>
      <CTextfield label="Username" innerRef={forwardedRef} />
      {/* ... other components */}
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 2">
Using Ref in parent component logic:

```tsx
import { useRef, useEffect } from 'react';
import { CTextfield, useForwardedRef } from "@ws-ui/webform-editor";

const MyComponent = () => {
  const inputRef = useRef<HTMLInputElement | null>(null);
  // highlight-next-line
  const forwardedRef = useForwardedRef(inputRef);

  useEffect(() => {
    // Access inputRef.current for additional logic
  }, [inputRef.current]);

  return (
    <div>
      <CTextfield label="Password" innerRef={forwardedRef} />
      {/* ... other components */}
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 3">
Using "forwardRef" with "useImperativeHandle":

```tsx
import { forwardRef, useImperativeHandle } from 'react';
import { CTextfield, useForwardedRef } from "@ws-ui/webform-editor";

const MyForwardedComponent = forwardRef((props, ref) => {
  // highlight-next-line
  const inputRef = useForwardedRef(ref);

  // Additional logic or methods exposed through ref
  useImperativeHandle(ref, () => ({
    focusInput: () => {
      inputRef.current?.focus();
    },
  }), [inputRef]);

  return (
    <div>
      <CTextfield label="Email" innerRef={inputRef} />
      {/* ... other components */}
    </div>
  );
});

const MyParentComponent = () => {
  const forwardedRef = useRef<HTMLInputElement | null>(null);

  return (
    <div>
      <MyForwardedComponent ref={forwardedRef} />
      <button onClick={() => forwardedRef.current?.focusInput()}>
        Focus Email Input
      </button>
      {/* ... other components */}
    </div>
  );
};
```

</TabItem>

</Tabs>





<!-- ################################################################################################################
#################################################### use-iterable-parent-node.ts ######################################################
#####################################################################################################################
-->

## use-iterable-parent-node.ts

<!-- ########### useCurrentIterableParentNode ############ -->
### `useIterableParentNodeGetter` Function

#### Purpose

A hook that retrieves information about the iterable parent node for a given node ID by traversing through the parent hierarchy until it identifies the first iterable parent node. It then extracts pertinent information, including the datasource and iterator.

#### Signature

```tsx
useIterableParentNodeGetter: ({
  parentId,
}: IUseIterableParentNodeGetterProps) => IUseIterableParentNodeReturnType | null;
```

#### Input

| **Parameter**  | **Type** | **Description**         |
|----------------|----------|-------------------------|
| `parentId` | `string` \| `null` | The ID of the node whose iterable parent node information needs to be retrieved. |

#### Output

| **Output**  | **Description**                 |
|-----------|---------------------------------|
| `IUseIterableParentNodeReturnType` \| `null`   | An object containing information about the iterable parent node, including datasource and iterator, or `null` if no iterable parent node is found. |

:::info
The `useIterableParentNodeGetter` function returns an object containing:

- `datasource`: An object containing information about the split datasource.
- `iterator`: A string representing the iterator used for the iterable parent node.

:::

<!-- ########### useIterableParentNode ############ -->
### `useIterableParentNode` Function

#### Purpose

A hook that encapsulates the logic of the [`useIterableParentNodeGetter`](#useiterableparentnodegetter-function) function, the useIterableParentNode hook automatically acquires the `parentId` by leveraging the currently selected node in the Craft.js editor.

#### Signature

```tsx
const useIterableParentNode: () => IUseIterableParentNodeReturnType | null;
```

#### Input (N/A)

#### Output

| **Output**  | **Description**                 |
|-----------|---------------------------------|
| `IUseIterableParentNodeReturnType` \| `null`   | An object containing information about the iterable parent node, including datasource and iterator, or `null` if no iterable parent node is found. |

#### Usage Example

```tsx
import { useIterableParentNode } from "@ws-ui/webform-editor";

//code
```

<!-- ########### useCurrentIterableParentNode ############ -->
### `useCurrentIterableParentNode` Function

#### Purpose

A hook that specifically retrieves information about the iterable parent node for the current node in the Craft.js editor, `useCurrentIterableParentNode` is a variant of [`useIterableParentNodeGetter`](#useiterableparentnodegetter-function).

#### Signature

```tsx
const useCurrentIterableParentNode: () => IUseIterableParentNodeReturnType | null;
```

#### Input (N/A)

#### Output

| **Output**  | **Description**                 |
|-----------|---------------------------------|
| `IUseIterableParentNodeReturnType` \| `null`   | An object containing information about the iterable parent node, including datasource and iterator, or `null` if no iterable parent node is found. |

#### Usage Example

```tsx
import { useCurrentIterableParentNode } from "@ws-ui/webform-editor";

//code
```




<!-- ################################################################################################################
#################################################### use-layout.ts ######################################################
#####################################################################################################################
-->

## use-layout.ts


<!-- ########### useLayout ############ -->
### `useLayout` Function

#### Purpose
A hook that provides methods and properties related to the layout mode of a webform.

#### Signature
```tsx
useLayout(): LayoutReturnType;
```

#### Input (N/A)

#### Output

| **Output**  | **Description**                 |
|-----------|---------------------------------|
| `LayoutReturnType`   | An object containing properties and methods related to the layout mode. |

:::info
The useLayout function returns an object with properties [`layout`](#layout) and [`isAiryMode`](#isairymode), along with methods [`getClassName`](#getclassnamecn-string) and [`toggle`](#togglechecked-boolean).
:::

<!-- ########### Properties ############ -->
#### Properties

##### `layout`

| **Type** | **Description** |
|----------|-----------------|
| `EDisplayMode` | The current layout mode, either `EDisplayMode.AIRY` or `EDisplayMode.COMPACT`. |

##### `isAiryMode`

| **Type** | **Description** |
|----------|-----------------|
| `boolean` | Indicates whether the current layout mode is in "Airy" mode. |

<!-- ########### Methods ############ -->
#### Methods

##### `toggle(checked: boolean)`

| **Input** | **Description** |
|----------------------|-----------------|
| `checked` (boolean) | Toggles the layout mode based on the provided boolean value. |

##### `getClassName(cn: string)`

| **Input** | **Output** | **Description** |
|----------------------|-----------------|-----------------|
| `cn` (string) | `string` | Returns a modified class name based on the current layout mode. If the layout is in "Airy" mode, it appends `--airy` to the class name. |

#### Usage Example

<Tabs>
<TabItem value="Example 1">
Basic usage:

```tsx
import { useLayout } from "@ws-ui/webform-editor";

const Example = () => {
  // highlight-next-line
  const { layout, isAiryMode, getClassName } = useLayout();

  return (
    <div>
      <p>Current Layout: {layout}</p>
      <p>Is Airy Mode: {isAiryMode ? 'Yes' : 'No'}</p>
      <p>Modified Class Name: {getClassName('my-container')}</p>
    </div>
  );
}
```

</TabItem>

<TabItem value="Example 2">
Toggle layout mode:

```tsx
import { useLayout } from "@ws-ui/webform-editor";

const Example = () => {
  // highlight-next-line
  const { toggle, isAiryMode } = useLayout();

  const handleToggle = () => {
    // highlight-next-line
    toggle(!isAiryMode);
  };

  return (
    <div>
      <p>Is Airy Mode: {isAiryMode ? 'Yes' : 'No'}</p>
      <button onClick={handleToggle}>
        Toggle Layout Mode
      </button>
    </div>
  );
}
```

</TabItem>

</Tabs>




<!-- ################################################################################################################
#################################################### use-methods.ts ######################################################
#####################################################################################################################
-->

## use-methods.ts


<!-- ########### useMethods ############ -->
### `useMethods` Function

#### Purpose
A hook that provides methods and state information related to webform datasources.

#### Signature
```tsx
useMethods(exclude?: 'shared' | 'private' | undefined): { methods: IMethodOption[] };
```

#### Input

| **Parameter**  | **Type** | **Description**         |
|----------------|----------|-------------------------|
| `exclude` | `shared` \| `private` \| `undefined` | Optional parameter to exclude specific types of datasources (e.g., `shared` or `private`). |

#### Output

| **Output**  | **Description**                 |
|-----------|---------------------------------|
| `{ methods: IMethodOption[] }`   | An object containing an array of method options for webform datasources. |

:::info
The `useMethods` function returns an object with a single property:

- `methods`: An array of `IMethodOption` arrays. Each array represents a category of methods, and `IMethodOption` is defined as follows:

  ```tsx
  interface IMethodOption {
    label: string;
    namespace?: string;
    options: IMethod[];
  }

  interface IMethod {
    label: string;
    value: string;
    exposed: boolean;
    dataclass: string;
    namespace?: string;
    datasource?: string;
  }
  ```

The `IMethodOption` arrays correspond to different categories of methods. Each `IMethodOption` object contains a `label` (category label), an optional `namespace`, and an array of `options`, where each `option` is an object containing information about a specific method (`label`, `value`, `exposed`, `dataclass`, `namespace`, and `datasource`).
:::

#### Usage Example

<Tabs>
<TabItem value="Example 1">
Basic usage:

```tsx
import { useMethods } from "@ws-ui/webform-editor";

const MyComponent = () => {
  // highlight-next-line
  const { methods } = useMethods();

  return (
    <div>
      <p>Available Methods:</p>
      <ul>
        {methods.map((method) => (
          <li key={method.label}>{method.label}</li>
        ))}
      </ul>
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 2">
Usage with exclusion:

```tsx
import { useMethods } from "@ws-ui/webform-editor";

const MyComponent = () => {
  // highlight-next-line
  const { methods } = useMethods('private');

  return (
    <div>
      <p>Available Methods (excluding private datasources):</p>
      <ul>
        {methods.map((method) => (
          <li key={method.label}>{method.label}</li>
        ))}
      </ul>
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 3">
Integration in a component:

```tsx
import { useMethods, MethodSelector, IMethod } from "@ws-ui/webform-editor";

const MyFormComponent = () => {
  // highlight-next-line
  const { methods } = useMethods();

  return (
    <div>
      <label>
        Select a Function:
        <MethodSelector
          options={methods}
          onChange={(selected: IMethod) => {
            // Handle the selected method
            console.log('Selected Method:', selected);
          }}
        />
      </label>
    </div>
  );
};
```

</TabItem>

</Tabs>





<!-- ################################################################################################################
#################################################### use-node-datasource.ts ######################################################
#####################################################################################################################
-->

## use-node-datasource.ts

<!-- ########### useNodeDatasource ############ -->
### `useNodeDatasource` Function

#### Purpose
A hook that provides a split datasource based on the specified filter criteria for a Craft.js node.

#### Signature
```tsx
useNodeDatasource({
  filter: string[];
}): ISplitDatasource | undefined;
```

#### Input

| **Parameter**  | **Type** | **Description**         |
|----------------|----------|-------------------------|
| `filter` | `string[]` | An array of display names to filter nodes. |

#### Output

| **Output**  | **Description**                 |
|-----------|---------------------------------|
| `ISplitDatasource` \| `undefined`   | A split datasource object or `undefined` if the node's display name doesn't match the filter criteria. |

:::info
The `ISplitDatasource` object contains the following properties:

- `id`: A string representing the ID of the datasource.
- `namespace`: A string representing the namespace of the datasource.
- `root`: A string representing the root of the datasource, derived from the ID.
- `original`: A string representing the original datasource ID, including both the namespace and the ID.
- `parts`: An optional array of strings representing different parts of the datasource.

:::


#### Usage Example

<Tabs>
<TabItem value="Example 1">
Basic usage:

```tsx
import { useNodeDatasource } from "@ws-ui/webform-editor";

const CDSAutoSuggestExample = () => {
  // highlight-next-line
  const source = useNodeDatasource({ filter: ['DataTable', 'Select Box'] });

  return (
    <div>
      {source ? (
        // Do something with the datasource
        <p>Current Datasource ID: {source.id}</p>
      ) : (
        // Handle the case where the node's display name doesn't match the filter criteria
        <p>No matching datasource found</p>
      )}
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 2">
Handling selected item change:

```tsx
import { useNodeDatasource } from "@ws-ui/webform-editor";

const CDSAutoSuggestExample = () => {
  // highlight-next-line
  const source = useNodeDatasource({ filter: ['DataTable', 'Select Box'] });

  const handleSelectedItemChange = ({ selectedItem: selected }) => {
    // Handle the selected item change
    console.log('Selected Item:', selected);
  };

  return (
    <div>
      {source ? (
        // Do something with the datasource
        <p>Current Datasource ID: {source.id}</p>
      ) : (
        // Handle the case where the node's display name doesn't match the filter criteria
        <p>No matching datasource found</p>
      )}
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 3">
Integrating with "useDsAutosugges":

```tsx
import { useNodeDatasource, useDsAutosuggest } from "@ws-ui/webform-editor";

const CDSAutoSuggestExample = () => {
  // highlight-next-line
  const source = useNodeDatasource({ filter: ['DataTable', 'Select Box'] });

  const { /* other variables from useDsAutosuggest */ } = useDsAutosuggest({
    source,
    // ... other configurations
  });

  return (
    <div>
      {source ? (
        // Do something with the datasource
        <p>Current Datasource ID: {source.id}</p>
      ) : (
        // Handle the case where the node's display name doesn't match the filter criteria
        <p>No matching datasource found</p>
      )}
    </div>
  );
};

```

</TabItem>

</Tabs>


<!-- ################################################################################################################
#################################################### use-node-tree.ts ######################################################
#####################################################################################################################
-->

## use-node-tree.ts


<!-- ########### useNodeTree ############ -->
### `useNodeTree` Function

#### Purpose
A hook that provides methods for parsing and creating templates from a node tree.

#### Signature
```tsx
useNodeTree(): {
  parseTemplate: (tree: IComponentTemplate) => NodeTree;
  createTemplate: (nodeTree: NodeTree, styles?: IWebFormStyleClass[]) => IComponentTemplate;
};
```

#### Input (N/A)

#### Output

| **Output**  | **Description**                 |
|-----------|---------------------------------|
| `NodeTreeMethods`   | An object containing methods for parsing and creating templates from a node tree. |

:::info
The `useNodeTree` function returns an object with two methods: [parseTemplate](#parsetemplate) and [createTemplate](#createtemplate).
:::

<!-- ###### Methods ############ -->
#### Methods

##### `parseTemplate`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `tree` (`IComponentTemplate`) | `NodeTree` | Parses a component template and returns the corresponding node tree. |


##### `createTemplate`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `nodeTree` (NodeTree), `styles` (IWebFormStyleClass[]) | `IComponentTemplate` | Creates a component template from a node tree and optional styles. |


#### Usage Example

```tsx
import { useNodeTree } from "@ws-ui/webform-editor";
import { useEditor, useNode } from '@ws-ui/craftjs-core';

const CreateTemplateExample = () => {
  // highlight-next-line
  const { createTemplate, parseTemplate } = useNodeTree();

  const { query } = useEditor();
  const { node } = useNode((node) => ({
    node,
  }));

  const nodeTree = query.node(node.id).toNodeTree();

  // highlight-start
  const serializedTree = createTemplate(nodeTree);
  const newTree = parseTemplate(serializedTree);
  // highlight-end

  // ... Rest of your component logic

  return (
    // JSX for your component
  );
};
```





<!-- ################################################################################################################
######################################### use-parent-node-child.ts ######################################################
#####################################################################################################################
-->

## use-parent-node-child.ts


<!-- ########### useParentNodeChild ############ -->
### `useParentNodeChild` Function

#### Purpose

A hook that provides information and actions for interacting with a child node within the context of its parent.

#### Signature
```tsx
useParentNodeChild(childName: string | undefined): {
  id: string | undefined;
  actions: {
    setProp: (cb: (props: any) => void) => void;
  };
} | null;
```

#### Input

| **Parameter**  | **Type** | **Description**         |
|----------------|----------|-------------------------|
| `childName` | `string` \| `undefined` | The name of the child node. |


#### Output

| **Output**  | **Description**                 |
|-----------|---------------------------------|
| `{ id, actions: { setProp } }` \| `null` | An object containing the child node's ID and actions to update its properties. Returns `null` if `childName` is falsy. |

:::info
The `useParentNodeChild` function returns an object with information for interacting with a child node, including its [`id`](#id) and a [`setProp`](#setprop) action.
:::


#### Properties

##### `id`

| **Type** | **Description** |
|----------|-----------------|
| `string` \| `undefined` | The ID of the child node. `undefined` if the child node does not exist. |

#### Actions

##### `setProp`

| **Input** | **Description** |
|-----------|-----------------|
| `cb: (props: any) => void` | A callback function that takes the current properties of the child node and modifies them. |

#### Usage Example

```tsx
import { useParentNodeChild } from "@ws-ui/webform-editor";

const ChildComponent = () => {
  const childName = "exampleChild";

  // highlight-next-line
  const { id, actions } = useParentNodeChild(childName);

  if (!id) {
    return <p>Child node not found.</p>;
  }

  // Render UI for the child node
  return (
    <div>
      <p>Child Node ID: {id}</p>
      <button onClick={() => actions.setProp((props) => ({ ...props, updated: true }))}>
        Update Child Node
      </button>
    </div>
  );
};
```




<!-- ################################################################################################################
########################################## use-parent-node-props.ts ######################################################
#####################################################################################################################
-->

## use-parent-node-props.ts

<!-- ########### useParentNodeProps ############ -->
### `useParentNodeProps` Function

#### Purpose

A hook that retrieves specific properties from the parent node in a Craft.js editor.

#### Signature
```tsx
useParentNodeProps<T extends Record<string, any>>(...propsName: string[]): T;
```

#### Input

| **Parameter**  | **Type** | **Description**         |
|----------------|----------|-------------------------|
| `propsName` | `string[]` | The names of the properties to retrieve from the parent node. |

#### Output

| **Output**  | **Description**                 |
|-----------|---------------------------------|
| `T`   | A typed object containing the specified properties from the parent node. |


#### Usage Example

```tsx
import { useParentNodeProps } from "@ws-ui/webform-editor";

interface IComponentProps {
  // props needed for your component
}

const Component = () => {
  // highlight-next-line
  const { orientation } = useParentNodeProps<IComponentProps>('orientation');

  // Your component logic here...

  return (
    <div>
      <p>Parent Node Orientation: {orientation}</p>
    </div>
  );
};
```





<!-- ################################################################################################################
#################################################### use-renderer.ts ######################################################
#####################################################################################################################
-->

## use-renderer.ts


<!-- ########### useServerSideRefHandler ############ -->
### `useServerSideRefHandler` Function

#### Purpose
A hook that provides a handler (`applySsRefChanges`) for applying changes to server-side references (ssRef) associated with a DOM element.

#### Signature
```tsx
useServerSideRefHandler(): {
  applySsRefChanges: (params: {
    domElement: HTMLElement | null | undefined;
    type: string;
    value: any;
  }) => void;
};
```

#### Input (N/A)

#### Output

| **Output**             | **Description**                                                                      |
|------------------------|----------------------------------------------------------------------------------------|
| [`applySsRefChanges`](#applyssrefchanges)    | Applies changes to a DOM element based on the server-side reference.                   |


<!-- ########### Methods ############ -->
#### Methods

##### `applySsRefChanges`

| **Input**       | **Output**             | **Description**       |
|-----------------|------------------------|------------------------|
| `domElement` (HTMLElement \| null \| undefined), `type` (string), `value` (any) | N/A	   | Applies changes to the DOM element based on the server-side reference. |

:::info
Supported Changes:

- Display: Modifies the display property of the element.
- addCSSClass/removeCSSClass: Adds or removes CSS classes from the element.
:::

#### Usage Example

<Tabs>
<TabItem value="Example 1">
Applying display changes:

```tsx
import { useEffect } from 'react';
import { useServerSideRefHandler } from "@ws-ui/webform-editor";

const DisplayExample = () => {
  // highlight-next-line
  const { applySsRefChanges } = useServerSideRefHandler();

  useEffect(() => {
    const updatedValue = { type: 'display', value: 'block' };

    // Apply changes to a DOM element
    applySsRefChanges({
      domElement: document.getElementById('exampleElementId'),
      type: updatedValue.type,
      value: updatedValue.value,
    });
  }, []);

  return (
    <div id="exampleElementId">
      {/* Content */}
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 2">
Applying CSS class changes:

```tsx
import { useEffect } from 'react';
import { useServerSideRefHandler } from "@ws-ui/webform-editor";

const CSSClassExample = () => {
  // highlight-next-line
  const { applySsRefChanges } = useServerSideRefHandler();

  useEffect(() => {
    const updatedValue = { type: 'addCSSClass', value: 'new-class' };

    // Apply changes to a DOM element
    applySsRefChanges({
      domElement: document.getElementById('exampleElementId'),
      type: updatedValue.type,
      value: updatedValue.value,
    });
  }, []);

  return (
    <div id="exampleElementId">
      {/* Content */}
    </div>
  );
};
```

</TabItem>

</Tabs>


<!-- ########### useRenderer ############ -->
### `useRenderer` Function

#### Purpose
A hook that facilitates rendering and event handling for a Craft.js node. It manages server-side references (ssRef) and auto-binds events to the corresponding DOM element.

#### Signature

```tsx
useRenderer({
  autoBindEvents?: boolean,
  omittedEvents?: string[];
}): {
  connectRenderer: (ref: any, omit?: string[]) => any;
  eventsToHandle: { [key: string]: Function };
  emit: (eventName: string, payload: any) => void;
};
```

#### Input
| **Parameter**           | **Type**       | **Description**                                |
|--------------------------|----------------|------------------------------------------------|
| `autoBindEvents`         | `boolean`      | Specifies whether events should be auto-bound. |
| `omittedEvents`          | `string[]`     | An array of event names to be omitted.          |

#### Output

| **Output**               | **Description**                                                                                           |
|--------------------------|-----------------------------------------------------------------------------------------------------------|
| `[HTMLElement \| null, { connectRenderer, eventsToHandle, emit}]`  | An object with methods for connecting, handling events, and emitting custom events. |

:::info
The `useRenderer` function returns a tuple with two elements:

- `HTMLElement | null`: The current DOM element or null. This represents the element to which the renderer is currently connected.
- An object providing methods to:

   - [Connect the renderer](#connectrenderer)

   - `eventsToHandle`: An object mapping event names to their corresponding handler functions.

   - `emit`: A function to emit a custom event with the specified name and payload.
:::


<!-- ########### Methods ############ -->
#### Methods

##### `connectRenderer`

| **Input**        | **Output** | **Description**     |
|------------------|------------|---------------------|
| `ref` (any), `omit` (string[]) | `any`   | Connects the renderer to a DOM element, optionally omits specified events during auto-binding.|

##### `parseEventName`

| **Input**                 | **Output** | **Description**                                                                             |
|---------------------------|------------|---------------------------------------------------------------------------------------------|
| `eventName` (string)      | `string`   | Parses event names, converting "onDoubleClick" to "ondblclick."                              |

##### `useEffect` (inside the hook)

Subscribes to changes in the `ssRefSubject` observable, applies changes to the DOM element based on server-side reference updates, and cleans up the subscription on component unmount. 


#### Usage Example

<Tabs>
<TabItem value="Example 1">
Basic rendering:

```tsx
import { useRef } from 'react';
import { useRenderer } from "@ws-ui/webform-editor";

const MyComponent = () => {
  // highlight-next-line
  const { connectRenderer } = useRenderer();
  const myRef = useRef();

  // Connect the renderer to the DOM element
  // highlight-next-line
  const connectedElement = connectRenderer(myRef.current);

  return (
    <div ref={myRef}>
      <h1>Hello, World!</h1>
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 2">
Auto-binding events:

```tsx
import { useRef } from 'react';
import { useRenderer } from "@ws-ui/webform-editor";

const MyComponent = () => {
  // highlight-next-line
  const { connectRenderer, eventsToHandle } = useRenderer({ autoBindEvents: true });
  const myRef = useRef();

  // Connect the renderer to the DOM element
  // highlight-next-line
  const connectedElement = connectRenderer(myRef.current);

  const handleClick = () => {
    console.log('Element clicked!');
  };

  // Assuming 'click' is automatically bound due to autoBindEvents
  // highlight-next-line
  eventsToHandle.click = handleClick;

  return (
    <div ref={myRef}>
      <button>Click me</button>
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 3">
Emitting custom events:

```tsx
import { useRef } from 'react';
import { useRenderer } from "@ws-ui/webform-editor";

const MyComponent = () => {
  // highlight-next-line
  const { connectRenderer, emit } = useRenderer();
  const myRef = useRef();

  // Connect the renderer to the DOM element
  // highlight-next-line
  const connectedElement = connectRenderer(myRef.current);

  // Emit a custom event
  const triggerCustomEvent = () => {
    // highlight-next-line
    emit('customEvent', { data: 'Some payload' });
  };

  return (
    <div ref={myRef}>
      <button onClick={triggerCustomEvent}>Trigger Custom Event</button>
    </div>
  );
};

```

</TabItem>

</Tabs>






<!-- ################################################################################################################
############################################ use-studio-panel.ts ######################################################
#####################################################################################################################
-->

## use-studio-panel.ts

<!-- ########### useStudioPanel ############ -->
### `useStudioPanel` Function

#### Purpose
A hook that provides state information and actions for managing the studio panel in a web form editor. The studio panel represents a dynamic side panel that displays information related to the selected element or component.

#### Signature
```tsx
useStudioPanel(): {
  type: string;
  isOpen: boolean;
  current: string;
  actions: {
    setState: (state: Partial<ITab['view']['panel']>) => void;
    setCurrent: (type: string, current: string) => void;
    close: () => void;
    open: () => void;
    openWithCurrent: (type: string, current: string) => void;
  };
};
```

#### Input (N/A)

#### Output

| **Type**  | **Description**                 |
|-----------|---------------------------------|
| `StudioPanelReturnType`   | An object containing the type, open state, current state, and actions to manipulate the studio panel. |

:::info
The `useStudioPanel` function returns an object with properties [`type`](#type), [`isOpen`](#isopen), [`current`](#current-1), and `actions` to manipulate the studio panel state.

The `actions` object includes methods for [updating the state](#setstate), [setting the current type and value](#setcurrent), [closing](#close), [opening](#open), and [opening with a specific type and current value](#openwithcurrent).

:::

 
<!-- ########### Properties ############ -->
#### Properties

##### `type`

| **Type** | **Description** |
|----------|-----------------|
| `string` | The type of the studio panel. |

##### `isOpen`

| **Type** | **Description** |
|----------|-----------------|
| `boolean` | A flag indicating whether the studio panel is open. |

##### `current`

| **Type** | **Description** |
|----------|-----------------|
| `string` | The current state of the studio panel. |


<!-- ########### Methods ############ -->
#### Methods

##### `setState`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `state` (Partial<ITab['view']['panel']>) | N/A | Sets the state of the studio panel with the provided partial state object. |

##### `setCurrent`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `type` (string), `current` (string) | N/A | Sets the type and current state of the studio panel. |

##### `close`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| N/A | N/A | Closes the studio panel. |

##### `open`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| N/A | N/A | Opens the studio panel. |

##### `openWithCurrent`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `type` (string), `current` (string) | N/A | Opens the studio panel with the specified type and current state. |

#### Usage Example

<Tabs>
<TabItem value="Example 1">
Open and close panel:

```tsx
import { useStudioPanel } from "@ws-ui/webform-editor";

const MyComponent = () => {
  // highlight-next-line
  const panel = useStudioPanel();

  return (
    <div>
      <button onClick={panel.actions.open}>Open Panel</button>
      <button onClick={panel.actions.close}>Close Panel</button>
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 2">
Set panel state:

```tsx
import { useStudioPanel } from "@ws-ui/webform-editor";

const MyComponent = () => {
  // highlight-next-line
  const panel = useStudioPanel();

  return (
    <div>
      <button onClick={() => panel.actions.setState({ isOpen: true })}>Open Panel</button>
      <button onClick={() => panel.actions.setState({ isOpen: false })}>Close Panel</button>
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 3">
Set current panel type and current value:

```tsx
import { useStudioPanel } from "@ws-ui/webform-editor";

const MyComponent = () => {
  // highlight-next-line
  const panel = useStudioPanel();

  return (
    <div>
      <button onClick={() => panel.actions.setCurrent('component', 'myComponent')}>
        Set Current Component
      </button>
      <button onClick={() => panel.actions.setCurrent('datasource', 'myDatasource')}>
        Set Current Datasource
      </button>
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 4">
Open panel with current type and current value:

```tsx
import { useStudioPanel } from "@ws-ui/webform-editor";

const MyComponent = () => {
  // highlight-next-line
  const panel = useStudioPanel();

  return (
    <div>
      <button onClick={() => panel.actions.openWithCurrent('component', 'myComponent')}>
        Open Panel with Current Component
      </button>
      <button onClick={() => panel.actions.openWithCurrent('datasource', 'myDatasource')}>
        Open Panel with Current Datasource
      </button>
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 5">
Perform multiple actions:

```tsx
import { useStudioPanel } from "@ws-ui/webform-editor";

const MyComponent = () => {
  // highlight-next-line
  const panel = useStudioPanel();

  return (
    <div>
      <button onClick={() => {
        panel.actions.open();
        panel.actions.setCurrent('component', 'myComponent');
      }}>
        Open Panel and Set Current Component
      </button>
      <button onClick={() => {
        panel.actions.close();
        panel.actions.setState({ isOpen: false });
      }}>
        Close Panel and Set State
      </button>
    </div>
  );
};
```

</TabItem>

</Tabs>





<!-- ################################################################################################################
########################################## use-style-adapter.ts ######################################################
#####################################################################################################################
-->

## use-style-adapter.ts

<!-- ########### useStylesEntity ############ -->
### `useStylesEntity` Function

#### Purpose
A hook that provides methods and state information for managing styles associated with a web form. It enables the manipulation of local and shared CSS classes, including actions such as duplicating, updating, and removing classes.

#### Signature
```tsx
useStylesEntity(): {
  actions: {
    duplicate: (_id: string, _includeChildren: boolean = false) => void;
    update: (
      id: string,
      cls: Partial<Omit<IWebFormStyleClass, 'name'>> &
        Pick<IWebFormStyleClass, 'name'>,
      updateOccurrences: boolean = true,
    ) => void;
    remove: (
      id: string,
      keepChildren: boolean,
      removeOccurrences: boolean,
    ) => void;
  };
  query: {
    getClass: (id: string) => IWebFormStyleClass | undefined;
    getClassReferences: (id: string) => string[] | undefined;
    populate: (style: IStyleDataTransferPayload) => {
      classname: string;
      children: Record<string, string>;
    };
  };
  state: {
    localCssClasses: IWebFormStyleClass[];
    sharedCssClasses: IWebFormStyleClass[];
    classesList: IWebFormStyleClass[];
  };
};
```

#### Input (N/A)

#### Output

| **Output**  | **Description**                 |
|-----------|---------------------------------|
| `StylesEntityReturnType`   | An object containing methods and state information for managing styles in a web form. |

:::info
The `useStylesEntity` function returns an object with the following structure:

- `actions`: An object containing methods for performing actions on styles, including [`duplicate`](#actionsduplicate), [`update`](#actionsupdate), and [`remove`](#actionsremove-1).
- `query`: An object containing methods for querying information about styles, including [`getClass`](#querygetclass), [`getClassReferences`](#querygetclassreferences), and [`populate`](#querypopulate).
- `state`: An object containing state information about styles, including `localCssClasses`, `sharedCssClasses`, and `classesList`.
:::


<!-- ########### Methods ############ -->
#### Properties

##### `localCssClasses`

| **Type**                | **Description**                                     |
|-------------------------|-----------------------------------------------------|
| `Array<any>`  | List of local CSS classes for the selected web form.|

##### `sharedCssClasses`

| **Type**                | **Description**                                     |
|-------------------------|-----------------------------------------------------|
| `Array<any>`  | List of shared CSS classes across web forms.        |

##### `classesList`

| **Type**                | **Description**                                     |
|-------------------------|-----------------------------------------------------|
| `Array<any>`  | Combined list of all styles, including local and shared.|

<!-- ########### Methods ############ -->
#### Methods

##### `actions.duplicate`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `_id` (string), `_includeChildren` (boolean) | N/A | Duplicates a style class. |

##### `actions.update`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `id` (string), `cls` (Partial<Omit<IWebFormStyleClass, 'name'>> & Pick<IWebFormStyleClass, 'name'>), `updateOccurrences` (boolean) | N/A | Updates a style class, optionally updating occurrences. |

##### `actions.remove`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `id` (string), `keepChildren` (boolean), `removeOccurrences` (boolean) | N/A | Removes a style class, optionally keeping children and removing occurrences. |

##### `query.getClass`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `id` (string) | `IWebFormStyleClass \| undefined` | Retrieves a style class by its ID. |

##### `query.getClassReferences`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `id` (string) | `string[] \| undefined` | Retrieves references to a style class. |

##### `query.populate`

| **Input** | **Output** | **Description** |
|-----------|------------|-----------------|
| `style` (IStyleDataTransferPayload) | `{ classname: string; children: Record<string, string> }` | Populates style information from a data transfer payload. |


#### Usage Example

<Tabs>
<TabItem value="Example 1">
Get the current CSS class and its details:

```tsx
import { useStylesEntity } from "@ws-ui/webform-editor";

const MyComponent = () => {
  // highlight-next-line
  const { query } = useStylesEntity();
  const cssClassId = 'yourCssClassId';

  const currentClass = query.getClass(cssClassId);

};
```

</TabItem>

<TabItem value="Example 2">
Update a CSS class:

```tsx
import { useStylesEntity } from "@ws-ui/webform-editor";

const MyComponent = () => {
  // highlight-next-line
  const { actions } = useStylesEntity();
  const cssClassId = 'yourCssClassId';

  actions.update(
    cssClassId,
    {
      name: 'NewClassName',
      content: 'NewClassContent',
    },
    true
  );
};
```

</TabItem>

<TabItem value="Example 3">
Remove a CSS class:

```tsx
import { useStylesEntity } from "@ws-ui/webform-editor";

const MyComponent = () => {
  // highlight-next-line
  const { actions } = useStylesEntity();
  const cssClassId = 'yourCssClassId';

  actions.remove(cssClassId, false, true);
};
```

</TabItem>

</Tabs>







<!-- ################################################################################################################
############################################ use-synced-state.ts ######################################################
#####################################################################################################################
-->

## use-synced-state.ts

<!-- ########### useSyncedState ############ -->
### `useSyncedState` Function

#### Purpose
A hook that manages a state variable, ensuring synchronization with the provided initial state. This is achieved by using the `useDidMountEffect` hook to compare the current state with the initial state and updating the state if they are not equal.

#### Signature
```tsx
useSyncedState<S>(
  initialState: S | (() => S),
): [S, Dispatch<SetStateAction<S>>];
```

#### Input

| **Parameter**  | **Type** | **Description**         |
|----------------|----------|-------------------------|
| `initialState` | `S` \| `(() => S)`  | The initial state value or a function that returns the initial state. |


#### Output

| **Output**  | **Description**                 |
|------------|---------------------------------|
| `[S, Dispatch<SetStateAction<S>>]`   | A tuple containing the current state and its corresponding `setState` function. |

:::info
The `useSyncedState` function returns a tuple with two elements:

- state: The current state value.

- setState: A function that can be used to update the state.
:::

#### Usage Example

<Tabs>
<TabItem value="Example 1">
Basic usage with a string state:

```tsx
import { useSyncedState } from "@ws-ui/webform-editor";

const ExampleComponent = () => {
  // highlight-next-line
  const [text, setText] = useSyncedState('Initial Text');

  return (
    <div>
      <input
        type="text"
        value={text}
        onChange={(e) => setText(e.target.value)}
      />
      <p>Current Text: {text}</p>
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 2">
Usage with dynamic initial state:

```tsx
import { useSyncedState } from "@ws-ui/webform-editor";

const ExampleComponent = () => {
  // highlight-next-line
  const [count, setCount] = useSyncedState(() => 0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 3">
Synchronize boolean state:

```tsx
import { useSyncedState } from "@ws-ui/webform-editor";

const ExampleComponent = () => {
  // highlight-next-line
  const [isChecked, setChecked] = useSyncedState(false);

  return (
    <div>
      <input
        type="checkbox"
        checked={isChecked}
        onChange={() => setChecked(!isChecked)}
      />
      <p>Checkbox is {isChecked ? 'checked' : 'unchecked'}</p>
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 4">
Using array state:

```tsx
import { useSyncedState } from "@ws-ui/webform-editor";

const ExampleComponent = () => {
  // highlight-next-line
  const [list, setList] = useSyncedState(['Apple', 'Banana', 'Orange']);

  return (
    <div>
      <ul>
        {list.map((item, index) => (
          <li key={index}>{item}</li>
        ))}
      </ul>
      <button onClick={() => setList([...list, 'New Fruit'])}>
        Add Fruit
      </button>
    </div>
  );
};
```

</TabItem>

<TabItem value="Example 5">
Complex state with object:

```tsx
import { useSyncedState } from "@ws-ui/webform-editor";

const ExampleComponent = () => {
  // highlight-next-line
  const [user, setUser] = useSyncedState({
    name: 'John Doe',
    age: 25,
    isAdmin: false,
  });

  return (
    <div>
      <p>Name: {user.name}</p>
      <p>Age: {user.age}</p>
      <p>Admin: {user.isAdmin ? 'Yes' : 'No'}</p>
      <button onClick={() => setUser({ ...user, age: user.age + 1 })}>
        Increment Age
      </button>
    </div>
  );
};
```

</TabItem>

</Tabs>





<!-- ################################################################################################################
####################################### use-welcome-tour-flags.ts ###################################################
#####################################################################################################################
-->

## use-welcome-tour-flags.ts

<!-- ########### useWelcomeTourFlags ############ -->
### `useWelcomeTourFlags` Function

#### Purpose
A hook that retrieves flags related to the welcome tour functionality from the Redux store.

#### Signature
```tsx
useWelcomeTourFlags(): {
  resizeSidebarSection: boolean | undefined;
}
```

#### Input (N/A)

#### Output

| **Output**              | **Description**                                     |
|-------------------------|-----------------------------------------------------|
| `WelcomeTourFlagsType`  | An object containing welcome tour flags.            |


:::info
The `useWelcomeTourFlags` function returns an object with a [`resizeSidebarSection`](#resizesidebarsection) boolean flag.
:::


<!-- ########### Flags ############ -->
#### Flags

##### `resizeSidebarSection`

| **Type**                | **Description**                                     |
|-------------------------|-----------------------------------------------------|
| `boolean` \| `undefined`  | Flag indicating whether the sidebar section is resizable. `undefined` if not set.|

#### Usage Example

```tsx
import { useWelcomeTourFlags } from "@ws-ui/webform-editor";

const MyComponent = () => {
  // highlight-next-line
  const { resizeSidebarSection } = useWelcomeTourFlags();

  console.log('Is Sidebar Section Resizable?', resizeSidebarSection);
};
```