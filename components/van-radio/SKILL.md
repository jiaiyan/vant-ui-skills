---
name: "van-radio"
description: "Radio component for single selection among multiple options. Invoke when user needs to implement radio buttons, radio groups, or custom radio selections."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Radio Component

Radio component for single selection among multiple options with flexible customization.

## When to Invoke

Invoke this skill when:
- User needs to implement a radio button group
- User wants to create single selection among multiple options
- User needs horizontal or vertical radio layouts
- User wants to customize radio icons, colors, or shapes
- User asks about radio integration with cells or forms

## Features

- **Flexible Layout**: Vertical or horizontal arrangement
- **Custom Shapes**: Round, square, or dot shapes
- **Custom Colors**: Customizable checked color
- **Custom Icons**: Support for custom icon slots
- **Label Position**: Left or right label positioning
- **Disabled State**: Disable individual or all radios
- **Cell Integration**: Works seamlessly with Cell component
- **Group Control**: RadioGroup for managing multiple radios

## API Reference

### Radio Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| name | Radio name, usually a unique string or number | `any` | - |
| shape | Can be set to `square` or `dot` | `string` | `round` |
| disabled | Whether to disable radio | `boolean` | `false` |
| label-disabled | Whether to disable label click | `boolean` | `false` |
| label-position | Can be set to `left` | `string` | `right` |
| icon-size | Icon size | `number \| string` | `20px` |
| checked-color | Checked color | `string` | `#1989fa` |

### RadioGroup Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model | Name of checked radio | `any` | - |
| disabled | Disable all radios | `boolean` | `false` |
| direction | Direction, can be set to `horizontal` | `string` | `vertical` |
| icon-size | Icon size of all radios | `number \| string` | `20px` |
| checked-color | Checked color of all radios | `string` | `#1989fa` |
| shape | Can be set to `square` or `dot` | `string` | `round` |

### Radio Events

| Event | Description | Parameters |
|-------|-------------|------------|
| click | Emitted when radio is clicked | `event: MouseEvent` |

### RadioGroup Events

| Event | Description | Parameters |
|-------|-------------|------------|
| change | Emitted when value changed | `name: string` |

### Radio Slots

| Name | Description | SlotProps |
|------|-------------|-----------|
| default | Custom label | `{ checked: boolean, disabled: boolean }` |
| icon | Custom icon | `{ checked: boolean, disabled: boolean }` |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-radio-group v-model="checked">
    <van-radio name="1">Radio 1</van-radio>
    <van-radio name="2">Radio 2</van-radio>
  </van-radio-group>
</template>

<script setup>
import { ref } from 'vue'

const checked = ref('1')
</script>
```

### Horizontal Layout

```vue
<template>
  <van-radio-group v-model="checked" direction="horizontal">
    <van-radio name="1">Radio 1</van-radio>
    <van-radio name="2">Radio 2</van-radio>
  </van-radio-group>
</template>

<script setup>
import { ref } from 'vue'

const checked = ref('1')
</script>
```

### Disabled State

```vue
<template>
  <van-radio-group v-model="checked" disabled>
    <van-radio name="1">Radio 1</van-radio>
    <van-radio name="2">Radio 2</van-radio>
  </van-radio-group>
</template>

<script setup>
import { ref } from 'vue'

const checked = ref('1')
</script>
```

### Custom Shape

```vue
<template>
  <van-radio-group v-model="checked" shape="square">
    <van-radio name="1">Square Radio 1</van-radio>
    <van-radio name="2">Square Radio 2</van-radio>
  </van-radio-group>

  <van-radio-group v-model="checked" shape="dot">
    <van-radio name="1">Dot Radio 1</van-radio>
    <van-radio name="2">Dot Radio 2</van-radio>
  </van-radio-group>
</template>

<script setup>
import { ref } from 'vue'

const checked = ref('1')
</script>
```

### Custom Color

```vue
<template>
  <van-radio-group v-model="checked">
    <van-radio name="1" checked-color="#ee0a24">Radio 1</van-radio>
    <van-radio name="2" checked-color="#ee0a24">Radio 2</van-radio>
  </van-radio-group>
</template>

<script setup>
import { ref } from 'vue'

const checked = ref('1')
</script>
```

### Custom Icon Size

```vue
<template>
  <van-radio-group v-model="checked">
    <van-radio name="1" icon-size="24px">Radio 1</van-radio>
    <van-radio name="2" icon-size="24px">Radio 2</van-radio>
  </van-radio-group>
</template>

<script setup>
import { ref } from 'vue'

const checked = ref('1')
</script>
```

### Custom Icon

```vue
<template>
  <van-radio-group v-model="checked">
    <van-radio name="1">
      Radio 1
      <template #icon="props">
        <img 
          class="img-icon" 
          :src="props.checked ? activeIcon : inactiveIcon" 
        />
      </template>
    </van-radio>
    <van-radio name="2">
      Radio 2
      <template #icon="props">
        <img 
          class="img-icon" 
          :src="props.checked ? activeIcon : inactiveIcon" 
        />
      </template>
    </van-radio>
  </van-radio-group>
</template>

<script setup>
import { ref } from 'vue'

const checked = ref('1')
const activeIcon = 'https://fastly.jsdelivr.net/npm/@vant/assets/user-active.png'
const inactiveIcon = 'https://fastly.jsdelivr.net/npm/@vant/assets/user-inactive.png'
</script>

<style scoped>
.img-icon {
  height: 20px;
}
</style>
```

### Left Label Position

```vue
<template>
  <van-radio-group v-model="checked">
    <van-radio name="1" label-position="left">Radio 1</van-radio>
    <van-radio name="2" label-position="left">Radio 2</van-radio>
  </van-radio-group>
</template>

<script setup>
import { ref } from 'vue'

const checked = ref('1')
</script>
```

### Disable Label Click

```vue
<template>
  <van-radio-group v-model="checked">
    <van-radio name="1" label-disabled>Radio 1</van-radio>
    <van-radio name="2" label-disabled>Radio 2</van-radio>
  </van-radio-group>
</template>

<script setup>
import { ref } from 'vue'

const checked = ref('1')
</script>
```

### Inside a Cell

```vue
<template>
  <van-radio-group v-model="checked">
    <van-cell-group inset>
      <van-cell title="Radio 1" clickable @click="checked = '1'">
        <template #right-icon>
          <van-radio name="1" />
        </template>
      </van-cell>
      <van-cell title="Radio 2" clickable @click="checked = '2'">
        <template #right-icon>
          <van-radio name="2" />
        </template>
      </van-cell>
    </van-cell-group>
  </van-radio-group>
</template>

<script setup>
import { ref } from 'vue'

const checked = ref('1')
</script>
```

### With Form Validation

```vue
<template>
  <van-form @submit="onSubmit">
    <van-field name="radio" label="Radio" :rules="[{ required: true, message: 'Please select' }]">
      <template #input>
        <van-radio-group v-model="radio" direction="horizontal">
          <van-radio name="1">Option 1</van-radio>
          <van-radio name="2">Option 2</van-radio>
        </van-radio-group>
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

const radio = ref('')

const onSubmit = () => {
  showToast('Submitted: ' + radio.value)
}
</script>
```

## Best Practices

1. **Use RadioGroup**: Always wrap radios in a RadioGroup for proper state management
2. **Unique Names**: Ensure each radio has a unique name within its group
3. **Accessibility**: Provide clear labels for better accessibility
4. **Mobile Optimization**: Use appropriate icon sizes for touch targets
5. **Form Integration**: Combine with Cell component for better mobile UX
6. **Visual Feedback**: Use custom colors to match your app's theme
7. **Disabled States**: Clearly indicate when options are unavailable
8. **Horizontal Layout**: Use horizontal layout for 2-3 options, vertical for more
