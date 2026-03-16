---
name: "van-tree-select"
description: "Tree select component for selecting from hierarchical data. Invoke when user needs to implement category selection with parent-child structure."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant TreeSelect Component

Tree select component used to select from a set of related data sets, commonly used for category selection.

## When to Invoke

Invoke this skill when:
- User needs to implement a category selector
- User wants to select from hierarchical data
- User needs single or multiple selection
- User wants to display items with parent-child structure
- User asks about custom content or badges

## Features

- **Hierarchical Data**: Support parent-child structure
- **Single/Multiple Selection**: Radio or checkbox mode
- **Custom Content**: Customize right panel content
- **Badge Support**: Show badges on navigation items
- **Disabled Items**: Disable specific items
- **Custom Height**: Adjustable component height

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model:main-active-index | Index of selected parent node | `number \| string` | `0` |
| v-model:active-id | Id of selected item(s) | `number \| string \| (number \| string)[]` | `0` |
| items | Data source | `TreeSelectItem[]` | `[]` |
| height | Component height | `number \| string` | `300` |
| max | Maximum selected items (multiple mode) | `number \| string` | `Infinity` |
| selected-icon | Selected icon name | `string` | `success` |

### Events

| Name | Description | Arguments |
|------|-------------|-----------|
| click-nav | Emitted when parent node is selected | `index: number` |
| click-item | Emitted when item is selected | `item: TreeSelectChild` |

### Slots

| Name | Description | SlotProps |
|------|-------------|-----------|
| nav-text | Custom parent node text | `item: TreeSelectChild` |
| content | Custom right content | - |

### Data Structure

```ts
interface TreeSelectItem {
  text: string;
  badge?: number | string;
  dot?: boolean;
  className?: string;
  disabled?: boolean;
  children?: TreeSelectChild[];
}

interface TreeSelectChild {
  text: string;
  id: number | string;
  disabled?: boolean;
}
```

### Types

```ts
import type { TreeSelectItem, TreeSelectChild, TreeSelectProps } from 'vant';
```

## Usage Examples

### Radio Mode (Single Selection)

```vue
<template>
  <van-tree-select
    v-model:active-id="activeId"
    v-model:main-active-index="activeIndex"
    :items="items"
  />
</template>

<script setup>
import { ref } from 'vue';

const activeId = ref(1);
const activeIndex = ref(0);
const items = ref([
  {
    text: 'Group 1',
    children: [
      { text: 'Delaware', id: 1 },
      { text: 'Florida', id: 2 },
      { text: 'Georgia', id: 3, disabled: true },
    ],
  },
  {
    text: 'Group 2',
    children: [
      { text: 'Alabama', id: 4 },
      { text: 'Kansas', id: 5 },
      { text: 'Louisiana', id: 6 },
    ],
  },
]);
</script>
```

### Multiple Selection

```vue
<template>
  <van-tree-select
    v-model:active-id="activeIds"
    v-model:main-active-index="activeIndex"
    :items="items"
  />
</template>

<script setup>
import { ref } from 'vue';

const activeIds = ref([1, 2]);
const activeIndex = ref(0);
const items = ref([
  {
    text: 'Group 1',
    children: [
      { text: 'Delaware', id: 1 },
      { text: 'Florida', id: 2 },
      { text: 'Georgia', id: 3, disabled: true },
    ],
  },
  {
    text: 'Group 2',
    children: [
      { text: 'Alabama', id: 4 },
      { text: 'Kansas', id: 5 },
      { text: 'Louisiana', id: 6 },
    ],
  },
]);
</script>
```

### Custom Content

```vue
<template>
  <van-tree-select
    v-model:main-active-index="activeIndex"
    height="55vw"
    :items="items"
  >
    <template #content>
      <van-image
        v-if="activeIndex === 0"
        src="https://fastly.jsdelivr.net/npm/@vant/assets/apple-1.jpeg"
      />
      <van-image
        v-if="activeIndex === 1"
        src="https://fastly.jsdelivr.net/npm/@vant/assets/apple-2.jpeg"
      />
    </template>
  </van-tree-select>
</template>

<script setup>
import { ref } from 'vue';

const activeIndex = ref(0);
const items = ref([
  { text: 'Group 1' },
  { text: 'Group 2' },
]);
</script>
```

### Show Badge

```vue
<template>
  <van-tree-select
    v-model:main-active-index="activeIndex"
    height="55vw"
    :items="items"
  />
</template>

<script setup>
import { ref } from 'vue';

const activeIndex = ref(0);
const items = ref([
  {
    text: 'Group 1',
    children: [
      { text: 'Delaware', id: 1 },
      { text: 'Florida', id: 2 },
    ],
    dot: true,
  },
  {
    text: 'Group 2',
    children: [
      { text: 'Alabama', id: 4 },
      { text: 'Kansas', id: 5 },
    ],
    badge: 5,
  },
]);
</script>
```

### With Events

```vue
<template>
  <van-tree-select
    v-model:active-id="activeId"
    v-model:main-active-index="activeIndex"
    :items="items"
    @click-nav="onClickNav"
    @click-item="onClickItem"
  />
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const activeId = ref(1);
const activeIndex = ref(0);
const items = ref([
  {
    text: 'Group 1',
    children: [
      { text: 'Delaware', id: 1 },
      { text: 'Florida', id: 2 },
    ],
  },
  {
    text: 'Group 2',
    children: [
      { text: 'Alabama', id: 4 },
      { text: 'Kansas', id: 5 },
    ],
  },
]);

const onClickNav = (index) => {
  showToast(`Clicked nav ${index}`);
};

const onClickItem = (item) => {
  showToast(`Clicked ${item.text}`);
};
</script>
```

### Limit Selection Count

```vue
<template>
  <van-tree-select
    v-model:active-id="activeIds"
    v-model:main-active-index="activeIndex"
    :items="items"
    :max="2"
  />
</template>

<script setup>
import { ref } from 'vue';

const activeIds = ref([1]);
const activeIndex = ref(0);
const items = ref([
  {
    text: 'Group 1',
    children: [
      { text: 'Delaware', id: 1 },
      { text: 'Florida', id: 2 },
      { text: 'Georgia', id: 3 },
    ],
  },
]);
</script>
```

## Best Practices

1. **Use appropriate height**: Set height based on your layout needs
2. **Limit selection**: Use `max` to limit selections in multiple mode
3. **Disabled items**: Disable unavailable options
4. **Badges for notifications**: Show badges for categories with updates
5. **Custom content**: Use content slot for rich displays
6. **Data structure**: Organize data with clear parent-child relationships
