---
name: "van-skeleton-avatar"
description: "Skeleton avatar placeholder component. Invoke when user needs to display avatar placeholders in custom skeleton layouts."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant SkeletonAvatar Component

Avatar placeholder component for use within custom skeleton layouts.

## When to Invoke

Invoke this skill when:
- User needs to create custom skeleton layouts with avatar placeholders
- User wants to display avatar loading states
- User asks about skeleton avatar customization
- User needs standalone avatar skeleton components

## Features

- **Size Customization**: Configurable avatar size
- **Shape Options**: Round or square shapes
- **Animation Support**: Inherits animation from parent skeleton
- **Standalone Usage**: Can be used independently in custom layouts

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| avatar-size | Size of avatar placeholder | `number \| string` | `32px` |
| avatar-shape | Shape of avatar placeholder, can be set to `square` | `string` | `round` |

### Types

```ts
import type { SkeletonAvatarProps, SkeletonAvatarShape } from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-skeleton-avatar />
</template>
```

### Custom Size

```vue
<template>
  <van-skeleton-avatar avatar-size="64px" />
</template>
```

### Square Shape

```vue
<template>
  <van-skeleton-avatar avatar-shape="square" />
</template>
```

### In Custom Layout

```vue
<template>
  <van-skeleton>
    <template #template>
      <div class="custom-skeleton">
        <van-skeleton-avatar avatar-size="48px" />
        <div class="content">
          <van-skeleton-title />
          <van-skeleton-paragraph />
        </div>
      </div>
    </template>
  </van-skeleton>
</template>

<style>
.custom-skeleton {
  display: flex;
  align-items: center;
  gap: 12px;
}

.content {
  flex: 1;
}
</style>
```

### Multiple Avatars

```vue
<template>
  <div class="avatar-group">
    <van-skeleton-avatar
      v-for="i in 5"
      :key="i"
      :avatar-size="40"
    />
  </div>
</template>

<style>
.avatar-group {
  display: flex;
  gap: 8px;
}
</style>
```

### Profile Card Skeleton

```vue
<template>
  <div class="profile-card-skeleton">
    <van-skeleton-avatar avatar-size="80px" />
    <div class="info">
      <van-skeleton-title title-width="50%" />
      <van-skeleton-paragraph row-width="70%" />
      <van-skeleton-paragraph row-width="40%" />
    </div>
  </div>
</template>

<style>
.profile-card-skeleton {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
}

.info {
  margin-top: 16px;
  text-align: center;
}
</style>
```

## Best Practices

1. **Match actual avatar size**: Set `avatar-size` to match the actual avatar dimensions
2. **Consistent shape**: Use the same shape as actual avatars in your design
3. **Combine with other skeleton components**: Use with SkeletonTitle and SkeletonParagraph for complete layouts
4. **Responsive sizing**: Consider using relative units for responsive designs
