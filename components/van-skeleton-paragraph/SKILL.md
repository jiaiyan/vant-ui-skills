---
name: "van-skeleton-paragraph"
description: "Skeleton paragraph placeholder component. Invoke when user needs to display text/paragraph placeholders in custom skeleton layouts."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant SkeletonParagraph Component

Paragraph placeholder component for use within custom skeleton layouts.

## When to Invoke

Invoke this skill when:
- User needs to create custom skeleton layouts with text placeholders
- User wants to display paragraph loading states
- User asks about skeleton paragraph customization
- User needs standalone paragraph skeleton components

## Features

- **Width Customization**: Configurable paragraph width
- **Round Style**: Option for rounded corners
- **Animation Support**: Inherits animation from parent skeleton
- **Standalone Usage**: Can be used independently in custom layouts

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| round | Whether to show round paragraph | `boolean` | `false` |
| row-width | Paragraph width | `string` | `100%` |

### Types

```ts
import type { SkeletonParagraphProps } from 'vant';
```

### CSS Variables

| Name | Default Value | Description |
|------|---------------|-------------|
| --van-skeleton-row-height | `16px` | Height of skeleton rows |
| --van-skeleton-row-background | `var(--van-active-color)` | Background color of rows |
| --van-skeleton-row-margin-top | `var(--van-padding-sm)` | Margin top of rows |
| --van-skeleton-duration | `1.2s` | Animation duration |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-skeleton-paragraph />
</template>
```

### Custom Width

```vue
<template>
  <van-skeleton-paragraph row-width="60%" />
</template>
```

### Round Style

```vue
<template>
  <van-skeleton-paragraph round />
</template>
```

### In Custom Layout

```vue
<template>
  <van-skeleton>
    <template #template>
      <div class="card-skeleton">
        <van-skeleton-title />
        <van-skeleton-paragraph />
        <van-skeleton-paragraph />
        <van-skeleton-paragraph row-width="60%" />
      </div>
    </template>
  </van-skeleton>
</template>

<style>
.card-skeleton {
  padding: 16px;
}
</style>
```

### Multiple Paragraphs

```vue
<template>
  <div class="paragraphs">
    <van-skeleton-paragraph />
    <van-skeleton-paragraph row-width="90%" />
    <van-skeleton-paragraph row-width="80%" />
    <van-skeleton-paragraph row-width="60%" />
  </div>
</template>

<style>
.paragraphs {
  display: flex;
  flex-direction: column;
  gap: 8px;
}
</style>
```

### Article Content Skeleton

```vue
<template>
  <div class="article-skeleton">
    <van-skeleton-title title-width="70%" />
    <div class="content">
      <van-skeleton-paragraph />
      <van-skeleton-paragraph />
      <van-skeleton-paragraph row-width="80%" />
    </div>
  </div>
</template>

<style>
.article-skeleton {
  padding: 16px;
}

.content {
  margin-top: 12px;
  display: flex;
  flex-direction: column;
  gap: 8px;
}
</style>
```

### Description List Skeleton

```vue
<template>
  <div class="description-list">
    <div v-for="i in 4" :key="i" class="item">
      <van-skeleton-paragraph row-width="30%" />
      <van-skeleton-paragraph row-width="60%" />
    </div>
  </div>
</template>

<style>
.description-list {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.item {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
</style>
```

### Card Content Skeleton

```vue
<template>
  <div class="card-content-skeleton">
    <van-skeleton-image image-size="100%" image-shape="square" />
    <div class="text-content">
      <van-skeleton-title title-width="50%" />
      <van-skeleton-paragraph row-width="100%" />
      <van-skeleton-paragraph row-width="80%" />
    </div>
  </div>
</template>

<style>
.card-content-skeleton {
  border-radius: 8px;
  overflow: hidden;
}

.text-content {
  padding: 12px;
  display: flex;
  flex-direction: column;
  gap: 8px;
}
</style>
```

## Best Practices

1. **Vary paragraph widths**: Use different widths for a more natural appearance
2. **Use round for modern design**: Use `round` prop for modern, rounded design
3. **Combine with other skeleton components**: Use with SkeletonTitle and SkeletonImage for complete layouts
4. **Match actual content**: Set widths to match actual paragraph lengths
