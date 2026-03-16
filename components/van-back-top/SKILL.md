---
name: "van-back-top"
description: "Back to top button component for easy navigation. Invoke when user needs to implement a back-to-top button for long pages."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Back Top Component

A button component that allows users to quickly scroll back to the top of the page.

## When to Invoke

Invoke this skill when:
- User needs to implement a back-to-top button
- User wants to show a button after scrolling down a certain distance
- User needs to customize the position of the back-to-top button
- User wants to scroll within a specific container
- User asks about scroll behavior or animation

## Features

- **Auto Show/Hide**: Automatically shows after scrolling past a threshold
- **Custom Position**: Customize right and bottom distance
- **Custom Content**: Support custom button content via slots
- **Target Container**: Scroll within a specific container instead of window
- **Immediate Scroll**: Option for instant scrolling without animation
- **Teleport**: Mount to a specific DOM element
- **Click Event**: Custom click handler support

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| target | Scroll target selector or DOM element | `string \| HTMLElement` | - |
| right | Right distance from page edge (px) | `number \| string` | `30` |
| bottom | Bottom distance from page edge (px) | `number \| string` | `40` |
| offset | Scroll offset threshold to show component | `number` | `200` |
| teleport | Target element to mount BackTop | `string \| Element` | `body` |
| immediate | Whether to scroll immediately without animation | `boolean` | `false` |
| z-index | Z-index of the component | `number \| string` | `100` |

### Events

| Name | Description | Arguments |
|------|-------------|-----------|
| click | Emitted when component is clicked | `event: MouseEvent` |

### Slots

| Name | Description |
|------|-------------|
| default | Custom button content |

### Types

```ts
import type { BackTopProps, BackTopThemeVars } from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <div>
    <van-cell v-for="item in list" :key="item" :title="`Item ${item}`" />
    <van-back-top />
  </div>
</template>

<script setup>
import { ref } from 'vue';

const list = ref([...Array(50).keys()]);
</script>
```

### Custom Position

```vue
<template>
  <div>
    <van-cell v-for="item in list" :key="item" :title="`Item ${item}`" />
    <van-back-top right="15vw" bottom="10vh" />
  </div>
</template>

<script setup>
import { ref } from 'vue';

const list = ref([...Array(50).keys()]);
</script>
```

### Custom Content

```vue
<template>
  <div>
    <van-cell v-for="item in list" :key="item" :title="`Item ${item}`" />
    <van-back-top class="custom-back-top">Back Top</van-back-top>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const list = ref([...Array(50).keys()]);
</script>

<style>
.custom-back-top {
  width: 80px;
  font-size: 14px;
  text-align: center;
}
</style>
```

### Scroll Within Container

```vue
<template>
  <div class="scroll-container">
    <van-cell v-for="item in list" :key="item" :title="`Item ${item}`" />
    <van-back-top target=".scroll-container" bottom="30vh" />
  </div>
</template>

<script setup>
import { ref } from 'vue';

const list = ref([...Array(50).keys()]);
</script>

<style>
.scroll-container {
  height: 60vh;
  overflow: auto;
}
</style>
```

### Immediate Scroll

```vue
<template>
  <div>
    <van-cell v-for="item in list" :key="item" :title="`Item ${item}`" />
    <van-back-top immediate />
  </div>
</template>

<script setup>
import { ref } from 'vue';

const list = ref([...Array(50).keys()]);
</script>
```

### With Click Event

```vue
<template>
  <div>
    <van-cell v-for="item in list" :key="item" :title="`Item ${item}`" />
    <van-back-top @click="handleClick" />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const list = ref([...Array(50).keys()]);

const handleClick = () => {
  showToast('Scrolled to top');
};
</script>
```

## Best Practices

1. **Set appropriate offset**: Use `offset` prop to control when the button appears (default 200px)
2. **Position carefully**: Avoid overlapping with other fixed elements
3. **Container scrolling**: Use `target` prop for scrollable containers
4. **Custom styling**: Use slots for custom button appearance
5. **Mobile optimization**: Consider safe areas on iOS devices
6. **Performance**: Use `immediate` for instant scrolling on long pages
