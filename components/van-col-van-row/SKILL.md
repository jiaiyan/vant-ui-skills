---
name: "van-col/van-row"
description: "Layout components based on 24-column grid system. Invoke when user needs to create responsive layouts, grid systems, or align elements."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Layout Components (van-col/van-row)

Quickly and easily create layouts with `van-row` and `van-col` based on a 24-column grid system.

## When to Invoke

Invoke this skill when:
- User needs to create a grid-based layout
- User wants to align elements horizontally or vertically
- User needs to set spacing between columns
- User wants to create responsive layouts
- User asks about flex layout alignment

## Features

- **24-Column Grid**: Flexible grid system based on 24 columns
- **Column Span**: Control column width with `span` attribute
- **Column Offset**: Set spacing on the left side of columns
- **Gutter Support**: Set horizontal and vertical spacing between columns
- **Flex Alignment**: Support for justify and align properties
- **Custom Tag**: Customize the HTML element tag

## API Reference

### Row Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| gutter | Grid spacing (px), supports array format `[horizontal, vertical]` | `number \| string \| Array` | - |
| tag | Custom element tag | `string` | `div` |
| justify | Flex main axis alignment: `start` `end` `center` `space-around` `space-between` | `string` | `start` |
| align | Flex cross axis alignment: `top` `center` `bottom` | `string` | `top` |
| wrap | Whether to wrap columns | `boolean` | `true` |

### Col Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| span | Number of columns the grid spans (1-24) | `number \| string` | - |
| offset | Number of spacing on the left side of the grid | `number \| string` | - |
| tag | Custom element tag | `string` | `div` |

### Row Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| click | Emitted when the row is clicked | `event: MouseEvent` |

### Col Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| click | Emitted when the col is clicked | `event: MouseEvent` |

### Types

```ts
import type { ColProps, RowProps, RowAlign, RowJustify } from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-row>
    <van-col span="8">span: 8</van-col>
    <van-col span="8">span: 8</van-col>
    <van-col span="8">span: 8</van-col>
  </van-row>

  <van-row>
    <van-col span="4">span: 4</van-col>
    <van-col span="10" offset="4">offset: 4, span: 10</van-col>
    <van-col span="6">span: 6</van-col>
  </van-row>

  <van-row>
    <van-col offset="12" span="12">offset: 12, span: 12</van-col>
  </van-row>
</template>
```

### Column Spacing

```vue
<template>
  <van-row gutter="20">
    <van-col span="8">span: 8</van-col>
    <van-col span="8">span: 8</van-col>
    <van-col span="8">span: 8</van-col>
  </van-row>
</template>
```

### Vertical Spacing

```vue
<template>
  <van-row :gutter="[20, 20]">
    <van-col span="12">span: 12</van-col>
    <van-col span="12">span: 12</van-col>
    <van-col span="12">span: 12</van-col>
    <van-col span="12">span: 12</van-col>
  </van-row>
</template>
```

### Justify Content

```vue
<template>
  <van-row justify="center">
    <van-col span="6">span: 6</van-col>
    <van-col span="6">span: 6</van-col>
    <van-col span="6">span: 6</van-col>
  </van-row>

  <van-row justify="end">
    <van-col span="6">span: 6</van-col>
    <van-col span="6">span: 6</van-col>
    <van-col span="6">span: 6</van-col>
  </van-row>

  <van-row justify="space-between">
    <van-col span="6">span: 6</van-col>
    <van-col span="6">span: 6</van-col>
    <van-col span="6">span: 6</van-col>
  </van-row>

  <van-row justify="space-around">
    <van-col span="6">span: 6</van-col>
    <van-col span="6">span: 6</van-col>
    <van-col span="6">span: 6</van-col>
  </van-row>
</template>
```

### Flex Alignment

```vue
<template>
  <van-row align="center" style="height: 100px">
    <van-col span="8">span: 8</van-col>
    <van-col span="8">span: 8</van-col>
    <van-col span="8">span: 8</van-col>
  </van-row>
</template>
```

### With Form Layout

```vue
<template>
  <van-form>
    <van-row gutter="12">
      <van-col span="12">
        <van-field v-model="firstName" label="First Name" />
      </van-col>
      <van-col span="12">
        <van-field v-model="lastName" label="Last Name" />
      </van-col>
    </van-row>
  </van-form>
</template>

<script setup>
import { ref } from 'vue';

const firstName = ref('');
const lastName = ref('');
</script>
```

### Responsive Layout

```vue
<template>
  <div class="responsive-layout">
    <van-row :gutter="[16, 16]">
      <van-col span="24" sm="12" md="8" lg="6">
        <div class="card">Card 1</div>
      </van-col>
      <van-col span="24" sm="12" md="8" lg="6">
        <div class="card">Card 2</div>
      </van-col>
      <van-col span="24" sm="12" md="8" lg="6">
        <div class="card">Card 3</div>
      </van-col>
      <van-col span="24" sm="12" md="8" lg="6">
        <div class="card">Card 4</div>
      </van-col>
    </van-row>
  </div>
</template>

<style scoped>
.card {
  padding: 16px;
  background: #f5f5f5;
  border-radius: 8px;
}
</style>
```

## Best Practices

1. **Use appropriate span values**: The total span should not exceed 24
2. **Combine with gutter**: Use gutter to create consistent spacing
3. **Responsive design**: Consider different screen sizes when setting spans
4. **Semantic tags**: Use appropriate HTML tags via the `tag` prop
5. **Avoid inline styles**: Use CSS classes for styling instead of inline styles
