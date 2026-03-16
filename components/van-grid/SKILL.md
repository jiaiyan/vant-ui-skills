---
name: "van-grid"
description: "Grid component for dividing pages into equal-width blocks. Invoke when user needs to create grid layouts for navigation or content display."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Grid Component

Grid component used to divide the page into blocks of equal width in the horizontal direction for displaying content or page navigation.

## When to Invoke

Invoke this skill when:
- User needs to create a grid layout with equal-width items
- User wants to implement a navigation menu with icons
- User needs to display items in a grid format
- User wants to customize grid columns and spacing
- User asks about square grid items or gutter settings

## Features

- **Flexible Columns**: Customize the number of columns
- **Square Items**: Option to make grid items square
- **Gutter Support**: Add spacing between items
- **Border Control**: Show or hide borders
- **Badge Support**: Display badges on grid items
- **Router Navigation**: Navigate to routes or URLs
- **Custom Content**: Full control over item content via slots
- **Direction Control**: Vertical or horizontal content arrangement

## API Reference

### Grid Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| column-num | Number of columns | `number \| string` | `4` |
| icon-size | Icon size | `number \| string` | `28px` |
| gutter | Spacing between items | `number \| string` | `0` |
| border | Whether to show border | `boolean` | `true` |
| center | Whether to center content | `boolean` | `true` |
| square | Whether to be square shape | `boolean` | `false` |
| clickable | Whether to show click feedback | `boolean` | `false` |
| direction | Content arrangement: `horizontal` or `vertical` | `string` | `vertical` |
| reverse | Whether to reverse icon and text position | `boolean` | `false` |

### GridItem Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| text | Text content | `string` | - |
| icon | Icon name or URL | `string` | - |
| icon-prefix | Icon className prefix | `string` | `van-icon` |
| icon-color | Icon color | `string` | - |
| dot | Whether to show red dot | `boolean` | `false` |
| badge | Content of the badge | `number \| string` | - |
| badge-props | Props of Badge component | `BadgeProps` | - |
| url | Link URL | `string` | - |
| to | Target route object | `string \| object` | - |
| replace | Whether to replace history | `boolean` | `false` |

### GridItem Events

| Name | Description | Arguments |
|------|-------------|-----------|
| click | Emitted when item is clicked | `event: MouseEvent` |

### GridItem Slots

| Name | Description |
|------|-------------|
| default | Custom content |
| icon | Custom icon |
| text | Custom text |

### Types

```ts
import type { GridProps, GridDirection, GridItemProps } from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-grid>
    <van-grid-item icon="photo-o" text="Photo" />
    <van-grid-item icon="photo-o" text="Photo" />
    <van-grid-item icon="photo-o" text="Photo" />
    <van-grid-item icon="photo-o" text="Photo" />
  </van-grid>
</template>
```

### Custom Column Number

```vue
<template>
  <van-grid :column-num="3">
    <van-grid-item 
      v-for="value in 6" 
      :key="value" 
      icon="photo-o" 
      text="Photo" 
    />
  </van-grid>
</template>
```

### Custom Content

```vue
<template>
  <van-grid :border="false" :column-num="3">
    <van-grid-item>
      <van-image src="https://fastly.jsdelivr.net/npm/@vant/assets/apple-1.jpeg" />
    </van-grid-item>
    <van-grid-item>
      <van-image src="https://fastly.jsdelivr.net/npm/@vant/assets/apple-2.jpeg" />
    </van-grid-item>
    <van-grid-item>
      <van-image src="https://fastly.jsdelivr.net/npm/@vant/assets/apple-3.jpeg" />
    </van-grid-item>
  </van-grid>
</template>
```

### Square Grid

```vue
<template>
  <van-grid square>
    <van-grid-item 
      v-for="value in 8" 
      :key="value" 
      icon="photo-o" 
      text="Photo" 
    />
  </van-grid>
</template>
```

### With Gutter

```vue
<template>
  <van-grid :gutter="10">
    <van-grid-item 
      v-for="value in 8" 
      :key="value" 
      icon="photo-o" 
      text="Photo" 
    />
  </van-grid>
</template>
```

### Horizontal Layout

```vue
<template>
  <van-grid direction="horizontal" :column-num="3">
    <van-grid-item icon="photo-o" text="Photo" />
    <van-grid-item icon="photo-o" text="Photo" />
    <van-grid-item icon="photo-o" text="Photo" />
  </van-grid>
</template>
```

### Route Navigation

```vue
<template>
  <van-grid clickable :column-num="2">
    <van-grid-item icon="home-o" text="Home" to="/" />
    <van-grid-item icon="search" text="Search" url="https://github.com" />
  </van-grid>
</template>
```

### Show Badge

```vue
<template>
  <van-grid :column-num="2">
    <van-grid-item icon="home-o" text="Home" dot />
    <van-grid-item icon="search" text="Search" badge="99+" />
  </van-grid>
</template>
```

### Custom Icon Color

```vue
<template>
  <van-grid :column-num="4">
    <van-grid-item icon="home-o" text="Home" icon-color="#1989fa" />
    <van-grid-item icon="search" text="Search" icon-color="#07c160" />
    <van-grid-item icon="setting-o" text="Settings" icon-color="#ee0a24" />
    <van-grid-item icon="user-o" text="User" icon-color="#ff976a" />
  </van-grid>
</template>
```

## Best Practices

1. **Choose appropriate columns**: Use 4 columns for mobile, 3 for tablets
2. **Use square for icons**: Enable `square` when displaying icon grids
3. **Add gutter for spacing**: Use `gutter` to create visual separation
4. **Enable clickable**: Add `clickable` for navigation items
5. **Limit items**: Keep grid items under 8 for better UX
6. **Use badges wisely**: Show badges only for items requiring attention
