---
name: "van-sticky"
description: "Sticky positioning component for fixed elements on scroll. Invoke when user needs to create sticky headers, navigation bars, or fixed position elements."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Sticky Component

The sticky component achieves the same effect as CSS `position: sticky`. When within screen range, it follows normal layout; when scrolled out of range, it stays fixed at the top or bottom of the screen.

## When to Invoke

Invoke this skill when:
- User needs to create sticky headers or navigation
- User wants elements to stay fixed while scrolling
- User needs sticky positioning within a container
- User asks about scroll-based fixed positioning
- User wants to create sticky toolbars or action bars

## Features

- **Top/Bottom Positioning**: Support for both top and bottom sticky
- **Offset Support**: Custom offset from top or bottom
- **Container Constraint**: Limit sticky behavior within a container
- **Scroll Events**: Events for scroll position and sticky state changes
- **Z-index Control**: Customizable z-index when sticky

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| position | Offset position, can be set to `bottom` | `string` | `top` |
| offset-top | Offset top, supports `px` `vw` `vh` `rem` unit, default `px` | `number \| string` | `0` |
| offset-bottom | Offset bottom, supports `px` `vw` `vh` `rem` unit, default `px` | `number \| string` | `0` |
| z-index | z-index when sticky | `number \| string` | `99` |
| container | Container DOM element | `Element` | - |

### Events

| Name | Description | Arguments |
|------|-------------|-----------|
| change | Emitted when sticky status changed | `isFixed: boolean` |
| scroll | Emitted when scrolling | `{ scrollTop: number, isFixed: boolean }` |

### Types

```ts
import type { StickyProps, StickyPosition } from 'vant';
```

### CSS Variables

| Name | Default Value | Description |
|------|---------------|-------------|
| --van-sticky-z-index | `99` | z-index when sticky |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-sticky>
    <van-button type="primary">Sticky Button</van-button>
  </van-sticky>
</template>
```

### Offset Top

```vue
<template>
  <van-sticky :offset-top="50">
    <van-button type="primary">Offset Top 50px</van-button>
  </van-sticky>
</template>
```

### Offset Bottom

```vue
<template>
  <van-sticky :offset-bottom="50" position="bottom">
    <van-button type="primary">Offset Bottom 50px</van-button>
  </van-sticky>
</template>
```

### Set Container

```vue
<template>
  <div ref="container" class="container">
    <van-sticky :container="container">
      <van-button type="warning">Sticky Within Container</van-button>
    </van-sticky>
    <div class="content">
      Scroll content here...
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const container = ref(null);
</script>

<style>
.container {
  height: 150px;
  overflow-y: auto;
  background: #f7f8fa;
}

.content {
  height: 500px;
  padding: 16px;
}
</style>
```

### Listen Events

```vue
<template>
  <van-sticky @change="onStickyChange" @scroll="onScroll">
    <div class="sticky-header" :class="{ fixed: isFixed }">
      {{ isFixed ? 'Fixed Header' : 'Normal Header' }}
    </div>
  </van-sticky>
</template>

<script setup>
import { ref } from 'vue';

const isFixed = ref(false);

const onStickyChange = (fixed) => {
  isFixed.value = fixed;
  console.log('Sticky state changed:', fixed);
};

const onScroll = ({ scrollTop, isFixed }) => {
  console.log('Scroll position:', scrollTop, 'Is fixed:', isFixed);
};
</script>

<style>
.sticky-header {
  padding: 16px;
  background: #fff;
  transition: all 0.3s;
}

.sticky-header.fixed {
  background: #1989fa;
  color: #fff;
}
</style>
```

### Sticky Navigation Bar

```vue
<template>
  <div class="page">
    <div class="header">
      <h1>Page Title</h1>
    </div>
    
    <van-sticky :offset-top="0">
      <van-tabs v-model:active="activeTab">
        <van-tab title="Tab 1">Content 1</van-tab>
        <van-tab title="Tab 2">Content 2</van-tab>
        <van-tab title="Tab 3">Content 3</van-tab>
      </van-tabs>
    </van-sticky>

    <div class="content">
      <p v-for="i in 50" :key="i">Scroll content line {{ i }}</p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const activeTab = ref(0);
</script>

<style>
.page {
  background: #f7f8fa;
}

.header {
  padding: 16px;
  background: #fff;
}

.content {
  padding: 16px;
  background: #fff;
}
</style>
```

### Sticky Action Bar

```vue
<template>
  <div class="product-page">
    <div class="product-info">
      <img src="product.jpg" alt="Product" />
      <h2>Product Name</h2>
      <p>Product description...</p>
    </div>

    <van-sticky position="bottom">
      <div class="action-bar">
        <van-button plain type="primary">Add to Cart</van-button>
        <van-button type="primary">Buy Now</van-button>
      </div>
    </van-sticky>
  </div>
</template>

<style>
.product-page {
  padding-bottom: 60px;
}

.product-info {
  padding: 16px;
}

.action-bar {
  display: flex;
  gap: 12px;
  padding: 12px 16px;
  background: #fff;
  box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.1);
}
</style>
```

### Sticky Section Headers

```vue
<template>
  <div class="list-with-headers">
    <div v-for="section in sections" :key="section.id" class="section">
      <van-sticky :offset-top="0">
        <div class="section-header">{{ section.title }}</div>
      </van-sticky>
      <div class="section-content">
        <van-cell
          v-for="item in section.items"
          :key="item.id"
          :title="item.name"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const sections = ref([
  { id: 1, title: 'Section A', items: [{ id: 1, name: 'Item A1' }, { id: 2, name: 'Item A2' }] },
  { id: 2, title: 'Section B', items: [{ id: 3, name: 'Item B1' }, { id: 4, name: 'Item B2' }] },
  { id: 3, title: 'Section C', items: [{ id: 5, name: 'Item C1' }, { id: 6, name: 'Item C2' }] },
]);
</script>

<style>
.section-header {
  padding: 10px 16px;
  background: #f7f8fa;
  font-weight: bold;
  color: #969799;
}

.section-content {
  background: #fff;
}
</style>
```

## Best Practices

1. **Use appropriate z-index**: Set z-index higher than other elements to prevent overlap
2. **Container constraint**: Use container prop to limit sticky behavior within a specific area
3. **Handle scroll events**: Use scroll events for dynamic UI updates
4. **Mobile optimization**: Consider safe areas on mobile devices when using offset
5. **Performance**: Avoid heavy computations in scroll event handlers
