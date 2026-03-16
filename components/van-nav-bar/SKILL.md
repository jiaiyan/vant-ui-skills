---
name: "van-nav-bar"
description: "Navigation bar component for page navigation. Invoke when user needs to implement top navigation bars with title, back button, and actions."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant NavBar Component

Navigation bar component that provides navigation function for the page, often used at the top of the page.

## When to Invoke

Invoke this skill when:
- User needs to implement a top navigation bar
- User wants to add a back button with navigation
- User needs to customize navigation bar title
- User wants to add action buttons on left or right
- User asks about fixed positioning or safe area adaptation

## Features

- **Title Display**: Support text title or custom content via slots
- **Back Button**: Built-in back arrow with customizable text
- **Action Buttons**: Add buttons on left or right side
- **Fixed Positioning**: Option to fix navigation bar at top
- **Safe Area**: Support top safe area adaptation for iOS
- **Border Control**: Show or hide bottom border
- **Disabled State**: Disable left or right buttons

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| title | Title text | `string` | `''` |
| left-text | Left button text | `string` | `''` |
| right-text | Right button text | `string` | `''` |
| left-disabled | Whether to disable left button | `boolean` | `false` |
| right-disabled | Whether to disable right button | `boolean` | `false` |
| left-arrow | Whether to show left arrow | `boolean` | `false` |
| border | Whether to show bottom border | `boolean` | `true` |
| fixed | Whether to fix at top | `boolean` | `false` |
| placeholder | Whether to generate placeholder when fixed | `boolean` | `false` |
| z-index | Z-index level | `number \| string` | `1` |
| safe-area-inset-top | Whether to enable top safe area adaptation | `boolean` | `false` |
| clickable | Whether to show click feedback | `boolean` | `true` |

### Slots

| Name | Description |
|------|-------------|
| title | Custom title |
| left | Custom left side content |
| right | Custom right side content |

### Events

| Name | Description | Arguments |
|------|-------------|-----------|
| click-left | Emitted when left button is clicked | `event: MouseEvent` |
| click-right | Emitted when right button is clicked | `event: MouseEvent` |

### Types

```ts
import type { NavBarProps } from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-nav-bar title="Title" />
</template>
```

### With Back Button

```vue
<template>
  <van-nav-bar
    title="Title"
    left-text="Back"
    left-arrow
    @click-left="onClickLeft"
  />
</template>

<script setup>
const onClickLeft = () => {
  history.back();
};
</script>
```

### With Right Button

```vue
<template>
  <van-nav-bar
    title="Title"
    left-text="Back"
    right-text="Button"
    left-arrow
    @click-left="onClickLeft"
    @click-right="onClickRight"
  />
</template>

<script setup>
import { showToast } from 'vant';

const onClickLeft = () => history.back();
const onClickRight = () => showToast('Button clicked');
</script>
```

### Custom Content with Slots

```vue
<template>
  <van-nav-bar title="Title" left-text="Back" left-arrow>
    <template #right>
      <van-icon name="search" size="18" />
    </template>
  </van-nav-bar>
</template>
```

### Fixed at Top

```vue
<template>
  <van-nav-bar
    title="Title"
    left-arrow
    fixed
    placeholder
    @click-left="onClickLeft"
  />
  <div class="content">
    <!-- Page content -->
  </div>
</template>

<script setup>
const onClickLeft = () => history.back();
</script>
```

### Disabled Buttons

```vue
<template>
  <van-nav-bar
    title="Title"
    left-text="Back"
    right-text="Button"
    left-arrow
    left-disabled
    right-disabled
  />
</template>
```

### Custom Title with Slot

```vue
<template>
  <van-nav-bar>
    <template #title>
      <div class="custom-title">
        <van-icon name="success" />
        <span>Custom Title</span>
      </div>
    </template>
  </van-nav-bar>
</template>

<style>
.custom-title {
  display: flex;
  align-items: center;
  gap: 8px;
}
</style>
```

### With Safe Area

```vue
<template>
  <van-nav-bar
    title="Title"
    left-arrow
    fixed
    safe-area-inset-top
    @click-left="onClickLeft"
  />
</template>

<script setup>
const onClickLeft = () => history.back();
</script>
```

## Best Practices

1. **Use placeholder**: Enable `placeholder` when using `fixed` to prevent content overlap
2. **Safe area**: Enable `safe-area-inset-top` for iOS devices with notches
3. **Back navigation**: Use `history.back()` or Vue Router for navigation
4. **Consistent styling**: Keep navigation bar consistent across all pages
5. **Action buttons**: Limit right-side actions to 1-2 buttons
6. **Disabled state**: Use disabled state for unavailable actions
