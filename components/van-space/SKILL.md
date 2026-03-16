---
name: "van-space"
description: "Space component for setting spacing between elements. Invoke when user needs to add consistent spacing between components or create flexible layouts."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Space Component

Set the spacing between elements with flexible direction and alignment options.

## When to Invoke

Invoke this skill when:
- User needs to add consistent spacing between elements
- User wants to create horizontal or vertical layouts with gaps
- User needs to align multiple elements
- User wants to create auto-wrapping button groups
- User asks about element spacing or alignment

## Features

- **Flexible Direction**: Horizontal or vertical spacing
- **Custom Size**: Support for custom spacing values
- **Alignment Options**: Multiple alignment modes (start, end, center, baseline)
- **Auto Wrap**: Automatic line wrapping for horizontal layout
- **Fill Mode**: Render as block element to fill parent

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| direction | Spacing direction | `'vertical' \| 'horizontal'` | `horizontal` |
| size | Spacing size, supports array for `[horizontal, vertical]` | `number \| string \| number[] \| string[]` | `8px` |
| align | Spacing alignment | `'start' \| 'end' \| 'center' \| 'baseline'` | - |
| wrap | Whether to wrap automatically (horizontal only) | `boolean` | `false` |
| fill | Whether to render as block element and fill parent | `boolean` | `false` |

### Slots

| Name | Description |
|------|-------------|
| default | Default slot for content |

### Types

```ts
import type { SpaceProps, SpaceSize, SpaceAlign } from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-space>
    <van-button type="primary">Button</van-button>
    <van-button type="primary">Button</van-button>
    <van-button type="primary">Button</van-button>
    <van-button type="primary">Button</van-button>
  </van-space>
</template>
```

### Vertical Direction

```vue
<template>
  <van-space direction="vertical" fill>
    <van-button type="primary" block>Button</van-button>
    <van-button type="primary" block>Button</van-button>
    <van-button type="primary" block>Button</van-button>
  </van-space>
</template>
```

### Custom Size

```vue
<template>
  <van-space :size="20">
    <van-button type="primary">Button</van-button>
    <van-button type="primary">Button</van-button>
    <van-button type="primary">Button</van-button>
  </van-space>

  <van-space size="2rem">
    <van-button type="primary">Button</van-button>
    <van-button type="primary">Button</van-button>
    <van-button type="primary">Button</van-button>
  </van-space>
</template>
```

### Alignment

```vue
<template>
  <van-radio-group
    v-model="align"
    direction="horizontal"
    style="margin-bottom: 16px"
  >
    <van-radio name="start">start</van-radio>
    <van-radio name="center">center</van-radio>
    <van-radio name="end">end</van-radio>
    <van-radio name="baseline">baseline</van-radio>
  </van-radio-group>

  <van-space :align="align" style="padding: 16px; background: #f3f2f5">
    <van-button type="primary">{{ align }}</van-button>
    <div style="padding: 40px 20px; background: #fff">Block</div>
  </van-space>
</template>

<script setup>
import { ref } from 'vue';

const align = ref('center');
</script>
```

### Auto Wrap

```vue
<template>
  <van-space wrap>
    <van-button type="primary" block>Button</van-button>
    <van-button type="primary" block>Button</van-button>
    <van-button type="primary" block>Button</van-button>
    <van-button type="primary" block>Button</van-button>
    <van-button type="primary" block>Button</van-button>
    <van-button type="primary" block>Button</van-button>
    <van-button type="primary" block>Button</van-button>
    <van-button type="primary" block>Button</van-button>
  </van-space>
</template>
```

### Mixed Horizontal and Vertical Spacing

```vue
<template>
  <van-space :size="[16, 8]" wrap>
    <van-button type="primary">Button 1</van-button>
    <van-button type="primary">Button 2</van-button>
    <van-button type="primary">Button 3</van-button>
    <van-button type="primary">Button 4</van-button>
    <van-button type="primary">Button 5</van-button>
  </van-space>
</template>
```

### Form Actions

```vue
<template>
  <van-space direction="vertical" fill>
    <van-field v-model="username" label="Username" />
    <van-field v-model="password" type="password" label="Password" />
    <van-space>
      <van-button type="primary" @click="handleSubmit">Submit</van-button>
      <van-button @click="handleReset">Reset</van-button>
    </van-space>
  </van-space>
</template>

<script setup>
import { ref } from 'vue';

const username = ref('');
const password = ref('');

const handleSubmit = () => {
  console.log('Submit:', { username: username.value, password: password.value });
};

const handleReset = () => {
  username.value = '';
  password.value = '';
};
</script>
```

### Card Grid

```vue
<template>
  <van-space direction="vertical" fill :size="16">
    <van-space fill :size="12">
      <div class="card">Card 1</div>
      <div class="card">Card 2</div>
    </van-space>
    <van-space fill :size="12">
      <div class="card">Card 3</div>
      <div class="card">Card 4</div>
    </van-space>
  </van-space>
</template>

<style scoped>
.card {
  flex: 1;
  padding: 20px;
  background: #f5f5f5;
  border-radius: 8px;
  text-align: center;
}
</style>
```

### Toolbar

```vue
<template>
  <van-space justify="space-between" fill>
    <van-space>
      <van-button size="small" icon="plus">Add</van-button>
      <van-button size="small" icon="edit">Edit</van-button>
    </van-space>
    <van-button size="small" icon="delete" type="danger">Delete</van-button>
  </van-space>
</template>
```

## Best Practices

1. **Use appropriate direction**: Use vertical for stacked content, horizontal for inline elements
2. **Consistent spacing**: Use the same size value throughout the application
3. **Combine with fill**: Use `fill` prop for full-width layouts
4. **Auto wrap for responsive**: Enable `wrap` for responsive button groups
5. **Alignment**: Use `align` prop for proper vertical alignment of different height elements
