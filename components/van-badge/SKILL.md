---
name: "van-badge"
description: "Badge component for displaying small badges or red dots on the top-right corner. Invoke when user needs to show notification counts, status indicators, or small badges."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Badge Component

Display a small badge or a red dot to the top-right of its child element.

## When to Invoke

Invoke this skill when:
- User needs to display notification counts or message numbers
- User wants to show status indicators with badges
- User needs to add red dots for new content reminders
- User wants to customize badge colors or positions
- User asks about badge max values or standalone usage

## Features

- **Multiple Types**: Number badges, text badges, and dot badges
- **Custom Colors**: Support custom background colors
- **Position Control**: Four position options (top-left, top-right, bottom-left, bottom-right)
- **Max Value**: Display `{max}+` when content exceeds maximum value
- **Offset Support**: Custom badge position offset
- **Standalone Mode**: Can be used without child elements
- **Custom Content**: Support custom content via slots

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| content | Badge content (Effective when `dot` is `false`) | `number \| string` | - |
| color | Background color | `string` | `#ee0a24` |
| dot | Whether to show dot | `boolean` | `false` |
| max | Max value, show `{max}+` when exceed, only works when content is number | `number \| string` | - |
| offset | Offset of badge dot, the two items of the array correspond to the horizontal and vertical offsets | `[number \| string, number \| string]` | - |
| show-zero | Whether to show badge when content is zero | `boolean` | `true` |
| position | Badge position, can be set to `top-left` `bottom-left` `bottom-right` | `string` | `top-right` |

### Slots

| Name | Description |
|------|-------------|
| default | Default slot for child element |
| content | Custom badge content |

### Types

```ts
import type { BadgeProps, BadgePosition } from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-badge :content="5">
    <div class="child" />
  </van-badge>
  <van-badge :content="10">
    <div class="child" />
  </van-badge>
  <van-badge content="Hot">
    <div class="child" />
  </van-badge>
  <van-badge dot>
    <div class="child" />
  </van-badge>
</template>

<style scoped>
.child {
  width: 40px;
  height: 40px;
  background: #f2f3f5;
  border-radius: 4px;
}
</style>
```

### Max Value

```vue
<template>
  <van-badge :content="20" max="9">
    <div class="child" />
  </van-badge>
  <van-badge :content="50" max="20">
    <div class="child" />
  </van-badge>
  <van-badge :content="200" max="99">
    <div class="child" />
  </van-badge>
</template>
```

### Custom Color

```vue
<template>
  <van-badge :content="5" color="#1989fa">
    <div class="child" />
  </van-badge>
  <van-badge :content="10" color="#1989fa">
    <div class="child" />
  </van-badge>
  <van-badge dot color="#1989fa">
    <div class="child" />
  </van-badge>
</template>
```

### Custom Content with Icon

```vue
<template>
  <van-badge>
    <div class="child" />
    <template #content>
      <van-icon name="success" class="badge-icon" />
    </template>
  </van-badge>
  <van-badge>
    <div class="child" />
    <template #content>
      <van-icon name="cross" class="badge-icon" />
    </template>
  </van-badge>
</template>

<style scoped>
.badge-icon {
  display: block;
  font-size: 10px;
  line-height: 16px;
}
</style>
```

### Custom Position

```vue
<template>
  <van-badge :content="10" position="top-left">
    <div class="child" />
  </van-badge>
  <van-badge :content="10" position="bottom-left">
    <div class="child" />
  </van-badge>
  <van-badge :content="10" position="bottom-right">
    <div class="child" />
  </van-badge>
</template>
```

### Standalone Usage

```vue
<template>
  <van-badge :content="20" />
  <van-badge :content="200" max="99" />
</template>
```

### With Icon Component

```vue
<template>
  <van-badge :content="5">
    <van-icon name="shopping-cart-o" size="26" />
  </van-badge>
</template>
```

## Common Issues

### 1. Badge Not Visible When Content is Zero

By default, badge shows when content is zero. Use `show-zero` to control:

```vue
<van-badge :content="0" :show-zero="false">
  <div class="child" />
</van-badge>
```

### 2. Custom Offset Position

Use `offset` to fine-tune badge position:

```vue
<van-badge :content="5" :offset="[10, 5]">
  <div class="child" />
</van-badge>
```

## Component Interactions

### With TabBar

```vue
<template>
  <van-tabbar v-model="active">
    <van-tabbar-item icon="home-o">Home</van-tabbar-item>
    <van-tabbar-item icon="search">Search</van-tabbar-item>
    <van-tabbar-item>
      <template #icon>
        <van-badge :content="5">
          <van-icon name="shopping-cart-o" />
        </van-badge>
      </template>
      Cart
    </van-tabbar-item>
  </van-tabbar>
</template>

<script setup>
import { ref } from 'vue';

const active = ref(0);
</script>
```

### With Icon

```vue
<template>
  <van-badge :content="notifications" max="99">
    <van-icon name="bell" size="24" @click="handleClick" />
  </van-badge>
</template>

<script setup>
import { ref } from 'vue';

const notifications = ref(10);

const handleClick = () => {
  console.log('Notification clicked');
};
</script>
```

## Best Practices

1. **Use appropriate badge types**: Use dot badges for simple status, number badges for counts
2. **Set reasonable max values**: Use `max` prop to prevent badge from becoming too wide
3. **Consider accessibility**: Add aria-label for screen readers when using icon-only badges
4. **Consistent positioning**: Use consistent badge positions across similar components
5. **Color semantics**: Use different colors to indicate different status types
