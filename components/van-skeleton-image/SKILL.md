---
name: "van-skeleton-image"
description: "Skeleton image placeholder component. Invoke when user needs to display image placeholders in custom skeleton layouts."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant SkeletonImage Component

Image placeholder component for use within custom skeleton layouts.

## When to Invoke

Invoke this skill when:
- User needs to create custom skeleton layouts with image placeholders
- User wants to display image loading states
- User asks about skeleton image customization
- User needs standalone image skeleton components

## Features

- **Size Customization**: Configurable image size
- **Shape Options**: Round or square shapes
- **Animation Support**: Inherits animation from parent skeleton
- **Standalone Usage**: Can be used independently in custom layouts

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| image-size | Size of image placeholder | `number \| string` | `32px` |
| image-shape | Shape of image placeholder, can be set to `square` | `string` | `round` |

### Types

```ts
import type { SkeletonImageProps, SkeletonImageShape } from 'vant';
```

### CSS Variables

| Name | Default Value | Description |
|------|---------------|-------------|
| --van-skeleton-image-size | `96px` | Image placeholder size |
| --van-skeleton-image-radius | `24px` | Image placeholder radius |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-skeleton-image />
</template>
```

### Custom Size

```vue
<template>
  <van-skeleton-image image-size="120px" />
</template>
```

### Square Shape

```vue
<template>
  <van-skeleton-image image-shape="square" />
</template>
```

### In Custom Layout

```vue
<template>
  <van-skeleton>
    <template #template>
      <div class="card-skeleton">
        <van-skeleton-image image-size="100%" image-shape="square" />
        <div class="content">
          <van-skeleton-title />
          <van-skeleton-paragraph />
        </div>
      </div>
    </template>
  </van-skeleton>
</template>

<style>
.card-skeleton {
  border-radius: 8px;
  overflow: hidden;
}

.content {
  padding: 12px;
}
</style>
```

### Image Gallery Skeleton

```vue
<template>
  <div class="gallery-skeleton">
    <van-skeleton-image
      v-for="i in 6"
      :key="i"
      image-size="100%"
      image-shape="square"
    />
  </div>
</template>

<style>
.gallery-skeleton {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 8px;
}
</style>
```

### Product Card Skeleton

```vue
<template>
  <div class="product-card-skeleton">
    <van-skeleton-image image-size="200px" image-shape="square" />
    <div class="product-info">
      <van-skeleton-paragraph row-width="80%" />
      <van-skeleton-paragraph row-width="40%" />
    </div>
  </div>
</template>

<style>
.product-card-skeleton {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.product-info {
  display: flex;
  flex-direction: column;
  gap: 8px;
}
</style>
```

### Banner Skeleton

```vue
<template>
  <div class="banner-skeleton">
    <van-skeleton-image
      :image-size="300"
      image-shape="square"
    />
  </div>
</template>

<style>
.banner-skeleton {
  width: 100%;
  border-radius: 12px;
  overflow: hidden;
}
</style>
```

## Best Practices

1. **Match actual image dimensions**: Set `image-size` to match the actual image dimensions
2. **Use square for rectangular images**: Use `image-shape="square"` for rectangular images
3. **Full width images**: Use `image-size="100%"` for full-width images
4. **Combine with other skeleton components**: Use with SkeletonTitle and SkeletonParagraph for complete layouts
