---
name: "van-action-bar"
description: "Action bar component for providing convenient interaction for page-related operations. Invoke when user needs to implement bottom action bars with icons and buttons."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Action Bar Component

Action bar component used to provide convenient interaction for page-related operations, commonly used at the bottom of product detail pages.

## When to Invoke

Invoke this skill when:
- User needs to implement a bottom action bar with icons and buttons
- User wants to create e-commerce product detail page actions
- User needs to add shopping cart, favorite, and buy buttons
- User wants to show badges on action bar icons
- User asks about action bar layout or safe area adaptation

## Features

- **Icon Buttons**: Support multiple icon buttons with text and badges
- **Action Buttons**: Support primary, warning, and danger type buttons
- **Badge Support**: Show dot or number badges on icons
- **Custom Colors**: Customize icon and button colors
- **Safe Area**: Automatic bottom safe area adaptation
- **Placeholder**: Optional placeholder element for fixed positioning
- **Router Support**: Navigate to routes or URLs

## API Reference

### ActionBar Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| safe-area-inset-bottom | Whether to enable bottom safe area adaptation | `boolean` | `true` |
| placeholder | Whether to generate a placeholder element | `boolean` | `false` |

### ActionBarIcon Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| text | Button text | `string` | - |
| icon | Icon name | `string` | - |
| color | Icon color | `string` | `#323233` |
| icon-class | Icon class name | `string \| Array \| object` | `''` |
| icon-prefix | Icon className prefix | `string` | `van-icon` |
| dot | Whether to show red dot | `boolean` | - |
| badge | Content of the badge | `number \| string` | - |
| badge-props | Props of Badge component | `BadgeProps` | - |
| url | Link URL | `string` | - |
| to | Target route object | `string \| object` | - |
| replace | Whether to replace history | `boolean` | `false` |
| disabled | Whether to disable icon | `boolean` | `false` |

### ActionBarButton Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| text | Button text | `string` | - |
| type | Button type: `default`, `primary`, `success`, `warning`, `danger` | `string` | `default` |
| color | Button color, support linear-gradient | `string` | - |
| icon | Left icon name | `string` | - |
| disabled | Whether to disable button | `boolean` | `false` |
| loading | Whether to show loading status | `boolean` | `false` |
| url | Link URL | `string` | - |
| to | Target route object | `string \| object` | - |
| replace | Whether to replace history | `boolean` | `false` |

### ActionBarIcon Slots

| Name | Description |
|------|-------------|
| default | Custom text |
| icon | Custom icon |

### ActionBarButton Slots

| Name | Description |
|------|-------------|
| default | Custom button content |

### Types

```ts
import type {
  ActionBarProps,
  ActionBarIconProps,
  ActionBarButtonProps,
} from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-action-bar>
    <van-action-bar-icon icon="chat-o" text="Chat" @click="onClickIcon" />
    <van-action-bar-icon icon="cart-o" text="Cart" @click="onClickIcon" />
    <van-action-bar-icon icon="shop-o" text="Shop" @click="onClickIcon" />
    <van-action-bar-button type="danger" text="Buy Now" @click="onClickButton" />
  </van-action-bar>
</template>

<script setup>
import { showToast } from 'vant';

const onClickIcon = () => showToast('Click Icon');
const onClickButton = () => showToast('Click Button');
</script>
```

### Icon Badge

```vue
<template>
  <van-action-bar>
    <van-action-bar-icon icon="chat-o" text="Chat" dot />
    <van-action-bar-icon icon="cart-o" text="Cart" badge="5" />
    <van-action-bar-icon icon="shop-o" text="Shop" badge="12" />
    <van-action-bar-button type="warning" text="Add to Cart" />
    <van-action-bar-button type="danger" text="Buy Now" />
  </van-action-bar>
</template>
```

### Custom Icon Color

```vue
<template>
  <van-action-bar>
    <van-action-bar-icon icon="chat-o" text="Chat" color="#ee0a24" />
    <van-action-bar-icon icon="cart-o" text="Cart" />
    <van-action-bar-icon icon="star" text="Collected" color="#ff5000" />
    <van-action-bar-button type="warning" text="Add to Cart" />
    <van-action-bar-button type="danger" text="Buy Now" />
  </van-action-bar>
</template>
```

### Custom Button Color

```vue
<template>
  <van-action-bar>
    <van-action-bar-icon icon="chat-o" text="Chat" />
    <van-action-bar-icon icon="shop-o" text="Shop" />
    <van-action-bar-button color="#be99ff" type="warning" text="Add to Cart" />
    <van-action-bar-button color="#7232dd" type="danger" text="Buy Now" />
  </van-action-bar>
</template>
```

### With Loading State

```vue
<template>
  <van-action-bar>
    <van-action-bar-icon icon="chat-o" text="Chat" />
    <van-action-bar-icon icon="cart-o" text="Cart" badge="5" />
    <van-action-bar-button 
      type="danger" 
      text="Buy Now" 
      :loading="loading"
      @click="handleBuy"
    />
  </van-action-bar>
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const loading = ref(false);

const handleBuy = async () => {
  loading.value = true;
  try {
    await new Promise(resolve => setTimeout(resolve, 2000));
    showToast('Purchase successful');
  } finally {
    loading.value = false;
  }
};
</script>
```

## Best Practices

1. **Use appropriate button types**: Use `danger` for primary actions like "Buy Now", `warning` for secondary actions like "Add to Cart"
2. **Show badges for cart items**: Display the cart item count using the `badge` prop
3. **Limit icon buttons**: Keep the number of icon buttons to 3-4 for better UX
4. **Safe area adaptation**: Enable `safe-area-inset-bottom` for iOS devices
5. **Loading states**: Use `loading` prop during async operations to prevent duplicate submissions
6. **Custom colors**: Use brand colors for buttons to match your application theme
