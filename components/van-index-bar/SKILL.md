---
name: "van-index-bar"
description: "Index bar component for indexed sorting display and quick positioning. Invoke when user needs to implement alphabetical or categorical navigation."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Index Bar Component

Index bar component used for indexed sorting display and quick positioning of lists, commonly used in contact lists or city selectors.

## When to Invoke

Invoke this skill when:
- User needs to implement an alphabetical index navigation
- User wants to create a contact list with quick access
- User needs a city selector with index sidebar
- User wants to implement sticky anchors for sections
- User asks about scroll positioning or index highlighting

## Features

- **Quick Navigation**: Jump to sections by clicking index
- **Custom Index List**: Define custom index characters or numbers
- **Sticky Anchors**: Anchors stick to top when scrolling
- **Highlight Color**: Customize active index color
- **Scroll Events**: Track scroll and selection events
- **Programmatic Control**: Scroll to specific index via methods

## API Reference

### IndexBar Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| index-list | Index character list | `(string \| number)[]` | `A-Z` |
| z-index | Z-index level | `number \| string` | `1` |
| sticky | Whether to enable anchor sticky top | `boolean` | `true` |
| sticky-offset-top | Anchor offset top when sticky | `number` | `0` |
| highlight-color | Index character highlight color | `string` | `#1989fa` |
| teleport | Target element to mount IndexBar | `string \| Element` | - |

### IndexAnchor Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| index | Index identifier | `number \| string` | - |

### IndexBar Events

| Name | Description | Arguments |
|------|-------------|-----------|
| select | Emitted when an index is selected | `index: number \| string` |
| change | Emitted when active index changes | `index: number \| string` |

### IndexBar Methods

| Name | Description | Arguments | Return Value |
|------|-------------|-----------|--------------|
| scrollTo | Scroll to target element | `index: number \| string` | - |

### IndexAnchor Slots

| Name | Description |
|------|-------------|
| default | Anchor content, shows index by default |

### Types

```ts
import type { IndexBarProps, IndexAnchorProps, IndexBarInstance } from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-index-bar>
    <van-index-anchor index="A" />
    <van-cell title="Aaron" />
    <van-cell title="Andy" />
    <van-cell title="Anna" />

    <van-index-anchor index="B" />
    <van-cell title="Ben" />
    <van-cell title="Bill" />
    <van-cell title="Bob" />

    <van-index-anchor index="C" />
    <van-cell title="Carol" />
    <van-cell title="Chris" />
    <van-cell title="Cindy" />
  </van-index-bar>
</template>
```

### Custom Index List

```vue
<template>
  <van-index-bar :index-list="indexList">
    <van-index-anchor index="1">Category 1</van-index-anchor>
    <van-cell title="Item 1-1" />
    <van-cell title="Item 1-2" />

    <van-index-anchor index="2">Category 2</van-index-anchor>
    <van-cell title="Item 2-1" />
    <van-cell title="Item 2-2" />

    <van-index-anchor index="3">Category 3</van-index-anchor>
    <van-cell title="Item 3-1" />
    <van-cell title="Item 3-2" />
  </van-index-bar>
</template>

<script setup>
import { ref } from 'vue';

const indexList = ref([1, 2, 3, 4, 5, 6, 7, 8, 9, 10]);
</script>
```

### With Sticky Offset

```vue
<template>
  <van-index-bar sticky :sticky-offset-top="50">
    <van-index-anchor index="A" />
    <van-cell title="Aaron" />
    <van-cell title="Andy" />

    <van-index-anchor index="B" />
    <van-cell title="Ben" />
    <van-cell title="Bill" />
  </van-index-bar>
</template>
```

### Custom Highlight Color

```vue
<template>
  <van-index-bar highlight-color="#ee0a24">
    <van-index-anchor index="A" />
    <van-cell title="Aaron" />

    <van-index-anchor index="B" />
    <van-cell title="Ben" />
  </van-index-bar>
</template>
```

### Programmatic Scroll

```vue
<template>
  <div>
    <van-button @click="scrollToB">Scroll to B</van-button>
    <van-index-bar ref="indexBarRef">
      <van-index-anchor index="A" />
      <van-cell title="Aaron" />
      <van-cell title="Andy" />

      <van-index-anchor index="B" />
      <van-cell title="Ben" />
      <van-cell title="Bill" />
    </van-index-bar>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const indexBarRef = ref();

const scrollToB = () => {
  indexBarRef.value?.scrollTo('B');
};
</script>
```

### With Events

```vue
<template>
  <van-index-bar @select="onSelect" @change="onChange">
    <van-index-anchor index="A" />
    <van-cell title="Aaron" />

    <van-index-anchor index="B" />
    <van-cell title="Ben" />
  </van-index-bar>
</template>

<script setup>
import { showToast } from 'vant';

const onSelect = (index) => {
  showToast(`Selected: ${index}`);
};

const onChange = (index) => {
  console.log('Active index:', index);
};
</script>
```

## Best Practices

1. **Use sticky anchors**: Enable `sticky` for better navigation experience
2. **Set appropriate offset**: Use `sticky-offset-top` when you have fixed headers
3. **Custom index list**: Use numbers or custom characters for non-alphabetical data
4. **Highlight color**: Match highlight color with your app theme
5. **Performance**: For large lists, consider virtual scrolling
6. **Accessibility**: Provide clear anchor labels for screen readers
