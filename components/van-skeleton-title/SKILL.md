---
name: "van-skeleton-title"
description: "Skeleton title placeholder component. Invoke when user needs to display title placeholders in custom skeleton layouts."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant SkeletonTitle Component

Title placeholder component for use within custom skeleton layouts.

## When to Invoke

Invoke this skill when:
- User needs to create custom skeleton layouts with title placeholders
- User wants to display title loading states
- User asks about skeleton title customization
- User needs standalone title skeleton components

## Features

- **Width Customization**: Configurable title width
- **Round Style**: Option for rounded corners
- **Animation Support**: Inherits animation from parent skeleton
- **Standalone Usage**: Can be used independently in custom layouts

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| round | Whether to show round title | `boolean` | `false` |
| title-width | Title width | `number \| string` | `40%` |

### Types

```ts
import type { SkeletonTitleProps } from 'vant';
```

### CSS Variables

| Name | Default Value | Description |
|------|---------------|-------------|
| --van-skeleton-title-width | `40%` | Width of title |
| --van-skeleton-row-height | `16px` | Height of skeleton rows |
| --van-skeleton-row-background | `var(--van-active-color)` | Background color |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-skeleton-title />
</template>
```

### Custom Width

```vue
<template>
  <van-skeleton-title title-width="60%" />
</template>
```

### Round Style

```vue
<template>
  <van-skeleton-title round />
</template>
```

### In Custom Layout

```vue
<template>
  <van-skeleton>
    <template #template>
      <div class="card-skeleton">
        <van-skeleton-title title-width="50%" />
        <van-skeleton-paragraph />
        <van-skeleton-paragraph />
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

### Header Skeleton

```vue
<template>
  <div class="header-skeleton">
    <van-skeleton-title title-width="30%" />
    <van-skeleton-title title-width="20%" />
  </div>
</template>

<style>
.header-skeleton {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
</style>
```

### Article Card Skeleton

```vue
<template>
  <div class="article-skeleton">
    <van-skeleton-title title-width="80%" />
    <van-skeleton-title title-width="60%" />
    <div class="meta">
      <van-skeleton-paragraph row-width="20%" />
      <van-skeleton-paragraph row-width="15%" />
    </div>
  </div>
</template>

<style>
.article-skeleton {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.meta {
  display: flex;
  gap: 16px;
  margin-top: 8px;
}
</style>
```

### Profile Header Skeleton

```vue
<template>
  <div class="profile-header-skeleton">
    <van-skeleton-avatar avatar-size="64px" />
    <div class="info">
      <van-skeleton-title title-width="40%" />
      <van-skeleton-paragraph row-width="60%" />
    </div>
  </div>
</template>

<style>
.profile-header-skeleton {
  display: flex;
  align-items: center;
  gap: 16px;
}

.info {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 8px;
}
</style>
```

## Best Practices

1. **Match actual title width**: Set `title-width` to match the actual title dimensions
2. **Use round for modern design**: Use `round` prop for modern, rounded design
3. **Combine with other skeleton components**: Use with SkeletonAvatar and SkeletonParagraph for complete layouts
4. **Responsive width**: Consider using percentage values for responsive designs
