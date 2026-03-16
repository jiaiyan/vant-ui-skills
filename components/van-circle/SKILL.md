---
name: "van-circle"
description: "Circular progress bar component with gradient color support. Invoke when user needs to display circular progress indicators or animated progress bars."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Circle Component

Circular progress bar component that supports gradient colors and animation effects.

## When to Invoke

Invoke this skill when:
- User needs to display circular progress indicators
- User wants to show percentage completion in circular form
- User needs gradient color progress bars
- User wants to customize progress bar size and stroke width
- User asks about clockwise or counter-clockwise progress

## Features

- **Animated Progress**: Smooth animation when rate changes
- **Gradient Support**: Support linear gradient colors
- **Custom Size**: Adjustable circle size and stroke width
- **Direction Control**: Clockwise or counter-clockwise
- **Start Position**: Four start positions (top, left, right, bottom)
- **Custom Text**: Display custom text in the center
- **Layer Color**: Custom background layer color

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model:current-rate | Current rate | `number` | - |
| rate | Target rate | `number \| string` | `100` |
| size | Circle size | `number \| string` | `100px` |
| color | Progress color, passing object to render gradient | `string \| object` | `#1989fa` |
| layer-color | Layer color | `string` | `white` |
| fill | Fill color | `string` | `none` |
| speed | Animate speed（rate/s） | `number \| string` | `0` |
| text | Text | `string` | - |
| stroke-width | Stroke width | `number \| string` | `40` |
| stroke-linecap | Stroke linecap, can be set to `square` `butt` | `string` | `round` |
| clockwise | Whether to be clockwise | `boolean` | `true` |
| start-position | Progress start position, can be set to `left`、`right`、`bottom` | `CircleStartPosition` | `top` |

### Slots

| Name | Description |
|------|-------------|
| default | Custom text content |

### Types

```ts
import type { CircleProps, CircleStartPosition } from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-circle
    v-model:current-rate="currentRate"
    :rate="30"
    :speed="100"
    :text="text"
  />
</template>

<script setup>
import { ref, computed } from 'vue';

const currentRate = ref(0);
const text = computed(() => currentRate.value.toFixed(0) + '%');
</script>
```

### Custom Width

```vue
<template>
  <van-circle
    v-model:current-rate="currentRate"
    :rate="rate"
    :stroke-width="60"
    text="Custom Width"
  />
</template>

<script setup>
import { ref } from 'vue';

const currentRate = ref(0);
const rate = ref(70);
</script>
```

### Custom Color

```vue
<template>
  <van-circle
    v-model:current-rate="currentRate"
    :rate="rate"
    layer-color="#ebedf0"
    text="Custom Color"
  />
</template>
```

### Gradient Color

```vue
<template>
  <van-circle
    v-model:current-rate="currentRate"
    :rate="rate"
    :color="gradientColor"
    text="Gradient"
  />
</template>

<script setup>
import { ref } from 'vue';

const currentRate = ref(0);
const rate = ref(70);
const gradientColor = {
  '0%': '#3fecff',
  '100%': '#6149f6',
};
</script>
```

### Counter Clockwise

```vue
<template>
  <van-circle
    v-model:current-rate="currentRate"
    :rate="rate"
    :clockwise="false"
    text="Counter Clockwise"
  />
</template>
```

### Custom Size

```vue
<template>
  <van-circle
    v-model:current-rate="currentRate"
    :rate="rate"
    size="120px"
    text="Custom Size"
  />
</template>
```

### Different Start Positions

```vue
<template>
  <van-circle
    v-model:current-rate="currentRate"
    :rate="rate"
    text="Left"
    start-position="left"
  />
  <van-circle
    v-model:current-rate="currentRate"
    :rate="rate"
    text="Right"
    start-position="right"
  />
  <van-circle
    v-model:current-rate="currentRate"
    :rate="rate"
    text="Bottom"
    start-position="bottom"
  />
</template>
```

### With Custom Content

```vue
<template>
  <van-circle v-model:current-rate="currentRate" :rate="rate">
    <div class="custom-content">
      <div class="rate">{{ currentRate.toFixed(0) }}%</div>
      <div class="label">Complete</div>
    </div>
  </van-circle>
</template>

<style scoped>
.custom-content {
  text-align: center;
}

.rate {
  font-size: 24px;
  font-weight: bold;
  color: #1989fa;
}

.label {
  font-size: 12px;
  color: #969799;
}
</style>
```

## Common Issues

### 1. Understanding Stroke Width

The `stroke-width` prop controls the width of the progress bar path in SVG:

```js
// viewBox size for SVG
const viewBox = 1000 + strokeWidth;

// The width of the Circle component, default is 100px
const circleWidth = 100;

// Final rendered progress bar width (px)
const pxWidth = (strokeWidth * circleWidth) / viewBox;
```

### 2. Animation Not Working

Make sure to set `speed` prop for animation:

```vue
<van-circle :rate="rate" :speed="100" />
```

### 3. Gradient Color Format

Gradient color should be an object with percentage keys:

```vue
<script setup>
const gradientColor = {
  '0%': '#3fecff',
  '50%': '#6149f6',
  '100%': '#ff0000',
};
</script>
```

## Component Interactions

### With Loading State

```vue
<template>
  <van-circle
    v-model:current-rate="currentRate"
    :rate="uploadProgress"
    :speed="100"
  >
    <template #default>
      <van-loading v-if="uploading" />
      <span v-else>{{ currentRate.toFixed(0) }}%</span>
    </template>
  </van-circle>
</template>

<script setup>
import { ref } from 'vue';

const currentRate = ref(0);
const uploadProgress = ref(0);
const uploading = ref(false);

const startUpload = () => {
  uploading.value = true;
  uploadProgress.value = 100;
};
</script>
```

### Multiple Progress Indicators

```vue
<template>
  <van-space>
    <van-circle
      v-model:current-rate="rate1"
      :rate="targetRate1"
      text="Download"
    />
    <van-circle
      v-model:current-rate="rate2"
      :rate="targetRate2"
      text="Upload"
    />
    <van-circle
      v-model:current-rate="rate3"
      :rate="targetRate3"
      text="Process"
    />
  </van-space>
</template>

<script setup>
import { ref } from 'vue';

const rate1 = ref(0);
const rate2 = ref(0);
const rate3 = ref(0);
const targetRate1 = ref(80);
const targetRate2 = ref(60);
const targetRate3 = ref(90);
</script>
```

## Best Practices

1. **Use appropriate size**: Choose circle size based on available space and importance
2. **Provide context**: Add descriptive text or labels to explain what the progress represents
3. **Consistent colors**: Use consistent colors for similar progress types
4. **Animation speed**: Set reasonable animation speed for better user experience
5. **Accessibility**: Ensure color contrast is sufficient for visibility
