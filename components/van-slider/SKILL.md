---
name: "van-slider"
description: "Slider component for selecting values within a range. Invoke when user needs to implement range selectors, volume controls, or custom slider interfaces."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Slider Component

Slider component for selecting values within a given range with single or dual thumb support.

## When to Invoke

Invoke this skill when:
- User needs to implement a range selector
- User wants to create volume or brightness controls
- User needs dual thumb range selection
- User wants to customize slider appearance
- User asks about vertical sliders or custom buttons

## Features

- **Single/Dual Thumb**: Support for single value or range selection
- **Custom Range**: Configurable min and max values
- **Step Size**: Adjustable step increments
- **Custom Styling**: Customizable bar height, colors, and button size
- **Custom Button**: Slot for custom button content
- **Vertical Mode**: Support for vertical orientation
- **Reverse Mode**: Reverse slider direction
- **Drag Events**: Start and end drag event notifications

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model | Current value | `number \| [number, number]` | `0` |
| max | Max value | `number \| string` | `100` |
| min | Min value | `number \| string` | `0` |
| step | Step size | `number \| string` | `1` |
| bar-height | Height of bar | `number \| string` | `2px` |
| button-size | Button size | `number \| string` | `24px` |
| active-color | Active color of bar | `string` | `#1989fa` |
| inactive-color | Inactive color of bar | `string` | `#e5e5e5` |
| range | Whether to enable dual thumb mode | `boolean` | `false` |
| reverse | Whether to reverse slider | `boolean` | `false` |
| disabled | Whether to disable slider | `boolean` | `false` |
| readonly | Whether to be readonly | `boolean` | `false` |
| vertical | Whether to display slider vertically | `boolean` | `false` |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| update:model-value | Emitted when value is changing | `value: number` |
| change | Emitted after value changed | `value: number` |
| drag-start | Emitted when start dragging | `event: TouchEvent` |
| drag-end | Emitted when end dragging | `event: TouchEvent` |

### Slots

| Name | Description | SlotProps |
|------|-------------|-----------|
| button | Custom button | `{ value: number, dragging: boolean }` |
| left-button | Custom left button in range mode | `{ value: number, dragging: boolean, dragIndex?: number }` |
| right-button | Custom right button in range mode | `{ value: number, dragging: boolean, dragIndex?: number }` |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-slider v-model="value" @change="onChange" />
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const value = ref(50)

const onChange = (value) => {
  showToast('Current value: ' + value)
}
</script>
```

### Dual Thumb

```vue
<template>
  <van-slider v-model="value" range @change="onChange" />
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const value = ref([10, 50])

const onChange = (value) => {
  showToast('Current value: ' + value)
}
</script>
```

### Custom Range

```vue
<template>
  <van-slider v-model="value" :min="-50" :max="50" />
</template>

<script setup>
import { ref } from 'vue'

const value = ref(0)
</script>
```

### Disabled State

```vue
<template>
  <van-slider v-model="value" disabled />
</template>

<script setup>
import { ref } from 'vue'

const value = ref(50)
</script>
```

### Step Size

```vue
<template>
  <van-slider v-model="value" :step="10" />
</template>

<script setup>
import { ref } from 'vue'

const value = ref(50)
</script>
```

### Custom Style

```vue
<template>
  <van-slider v-model="value" bar-height="4px" active-color="#ee0a24" />
</template>

<script setup>
import { ref } from 'vue'

const value = ref(50)
</script>
```

### Custom Button

```vue
<template>
  <van-slider v-model="value">
    <template #button>
      <div class="custom-button">{{ value }}</div>
    </template>
  </van-slider>
</template>

<script setup>
import { ref } from 'vue'

const value = ref(50)
</script>

<style scoped>
.custom-button {
  width: 26px;
  color: #fff;
  font-size: 10px;
  line-height: 18px;
  text-align: center;
  background-color: var(--van-primary-color);
  border-radius: 100px;
}
</style>
```

### Vertical Slider

```vue
<template>
  <div :style="{ height: '150px' }">
    <van-slider v-model="value" vertical @change="onChange" />
    <van-slider
      v-model="value2"
      range
      vertical
      style="margin-left: 100px;"
      @change="onChange"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const value = ref(50)
const value2 = ref([10, 50])

const onChange = (value) => {
  showToast('Current value: ' + value)
}
</script>
```

### Volume Control

```vue
<template>
  <div class="volume-control">
    <van-icon :name="volumeIcon" />
    <van-slider 
      v-model="volume" 
      :max="100"
      active-color="#1989fa"
      @change="onVolumeChange"
    />
    <span class="volume-value">{{ volume }}%</span>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const volume = ref(50)

const volumeIcon = computed(() => {
  if (volume.value === 0) return 'volume-o'
  if (volume.value < 50) return 'volume'
  return 'volume'
})

const onVolumeChange = (val) => {
  console.log('Volume changed to:', val)
}
</script>

<style scoped>
.volume-control {
  display: flex;
  align-items: center;
  padding: 16px;
  gap: 12px;
}

.volume-value {
  min-width: 40px;
  text-align: right;
  font-size: 14px;
  color: #323233;
}
</style>
```

### Price Range Selector

```vue
<template>
  <div class="price-range">
    <div class="price-header">
      <span>Price Range</span>
      <span class="price-values">${{ value[0] }} - ${{ value[1] }}</span>
    </div>
    <van-slider 
      v-model="value" 
      range 
      :min="0" 
      :max="1000" 
      :step="10"
      active-color="#ee0a24"
      @change="onPriceChange"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue'

const value = ref([100, 500])

const onPriceChange = (val) => {
  console.log('Price range:', val)
}
</script>

<style scoped>
.price-range {
  padding: 16px;
}

.price-header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 16px;
  font-size: 14px;
  color: #323233;
}

.price-values {
  color: #ee0a24;
  font-weight: bold;
}
</style>
```

### With Form

```vue
<template>
  <van-form @submit="onSubmit">
    <van-field name="slider" label="Brightness">
      <template #input>
        <van-slider v-model="brightness" />
      </template>
    </van-field>
    <div style="margin: 16px;">
      <van-button round block type="primary" native-type="submit">
        Submit
      </van-button>
    </div>
  </van-form>
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const brightness = ref(50)

const onSubmit = () => {
  showToast('Brightness: ' + brightness.value)
}
</script>
```

## Best Practices

1. **Appropriate Range**: Set meaningful min and max values for your use case
2. **Step Size**: Use appropriate step sizes for different scenarios
3. **Visual Feedback**: Show current value with custom button or label
4. **Touch Targets**: Ensure button size is adequate for touch interaction
5. **Accessibility**: Provide labels and value announcements for screen readers
6. **Vertical Space**: Ensure adequate height for vertical sliders
7. **Dual Thumb**: Use range mode for interval selection
8. **Performance**: Debounce change events for expensive operations
