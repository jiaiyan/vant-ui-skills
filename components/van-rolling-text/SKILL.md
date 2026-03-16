---
name: "van-rolling-text"
description: "Rolling text animation component for numbers and text. Invoke when user needs to create animated number counters, rolling text effects, or slot machine-style animations."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant RollingText Component

Rolling text animation component that can roll numbers and other types of text with smooth animation effects.

## When to Invoke

Invoke this skill when:
- User needs to create animated number counters
- User wants to implement slot machine-style rolling effects
- User needs to display rolling text animations
- User wants to create countdown or count-up animations
- User asks about number animation effects

## Features

- **Number Rolling**: Roll from start number to target number
- **Direction Control**: Support up and down rolling directions
- **Stop Order**: Control the order of stopping animation for each digit
- **Non-numeric Text**: Support rolling non-numeric text arrays
- **Custom Style**: Customizable height, color, and font size
- **Manual Control**: Start and reset methods for programmatic control
- **Auto Start**: Option to automatically start animation on mount

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| start-num | Start number | `number` | `0` |
| target-num | Target number | `number` | - |
| text-list | Text array for non-numeric rolling | `string[]` | `[]` |
| duration | Duration of the animation in seconds | `number` | `2` |
| direction | Rolling direction, `down` or `up` | `string` | `down` |
| auto-start | Whether to start the animation automatically | `boolean` | `true` |
| stop-order | Order of stopping animation, `ltr` or `rtl` | `string` | `ltr` |
| height | Height of digit in pixels | `number` | `40` |

### Methods

Use ref to get RollingText instance and call instance methods.

| Name | Description | Arguments | Return Value |
|------|-------------|-----------|--------------|
| start | Start the animation | - | - |
| reset | Reset the animation | - | - |

### Types

```ts
import type {
  RollingTextProps,
  RollingTextInstance,
  RollingTextDirection,
  RollingTextStopOrder,
} from 'vant';
```

### CSS Variables

| Name | Default Value | Description |
|------|---------------|-------------|
| --van-rolling-text-background | `inherit` | Background color of a single digit |
| --van-rolling-text-color | `var(--van-text-color)` | Color of the number |
| --van-rolling-text-font-size | `var(--van-font-size-md)` | Font size of the number |
| --van-rolling-text-gap | `0px` | Spacing between digits |
| --van-rolling-text-item-width | `15px` | Width of a single digit |
| --van-rolling-text-item-border-radius | `0px` | Border radius of a single digit |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-rolling-text :start-num="0" :target-num="123" />
</template>
```

### Set Rolling Direction

```vue
<template>
  <van-rolling-text :start-num="0" :target-num="432" direction="up" />
</template>
```

### Set Stop Order

```vue
<template>
  <van-rolling-text :start-num="0" :target-num="54321" stop-order="rtl" />
</template>
```

### Roll Non-numeric Text

```vue
<template>
  <van-rolling-text :text-list="textList" :duration="1" />
</template>

<script setup>
import { ref } from 'vue';

const textList = ref([
  'aaaaa',
  'bbbbb',
  'ccccc',
  'ddddd',
  'eeeee',
  'fffff',
  'ggggg',
]);
</script>
```

### Custom Style

```vue
<template>
  <van-rolling-text
    class="my-rolling-text"
    :height="54"
    :start-num="12345"
    :target-num="54321"
  />
</template>

<style>
.my-rolling-text {
  --van-rolling-text-background: #1989fa;
  --van-rolling-text-color: white;
  --van-rolling-text-font-size: 24px;
  --van-rolling-text-gap: 6px;
  --van-rolling-text-item-border-radius: 5px;
  --van-rolling-text-item-width: 40px;
}
</style>
```

### Manual Control

```vue
<template>
  <van-rolling-text
    ref="rollingTextRef"
    :start-num="0"
    :target-num="54321"
    :auto-start="false"
  />
  <van-grid clickable :column-num="3">
    <van-grid-item icon="play-circle-o" text="Start" @click="start" />
    <van-grid-item icon="replay" text="Reset" @click="reset" />
  </van-grid>
</template>

<script setup>
import { ref } from 'vue';

const rollingTextRef = ref(null);

const start = () => {
  rollingTextRef.value?.start();
};

const reset = () => {
  rollingTextRef.value?.reset();
};
</script>
```

### Counter Animation

```vue
<template>
  <div class="counter-demo">
    <van-rolling-text
      ref="counterRef"
      :start-num="startValue"
      :target-num="targetValue"
      :duration="2"
    />
    <van-button type="primary" @click="animate">
      Animate
    </van-button>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const counterRef = ref(null);
const startValue = ref(0);
const targetValue = ref(9999);

const animate = () => {
  counterRef.value?.reset();
  setTimeout(() => {
    counterRef.value?.start();
  }, 100);
};
</script>
```

## Best Practices

1. **Use appropriate duration**: Set duration based on the number of digits for smooth animation
2. **Manual control for complex scenarios**: Use `auto-start="false"` when you need precise control
3. **Custom styling**: Use CSS variables for consistent styling across the app
4. **Text array consistency**: Ensure all items in `text-list` have the same length
5. **Reset before restart**: Call `reset()` before `start()` when re-animating
