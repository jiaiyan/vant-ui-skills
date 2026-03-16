---
name: "van-notice-bar"
description: "Notice bar component for displaying scrolling notifications. Invoke when user needs to show announcements, alerts, or continuous scrolling messages."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant NoticeBar Component

Used to display a group of message notifications in a continuous loop.

## When to Invoke

Invoke this skill when:
- User needs to display scrolling announcements
- User wants to show notification bars with icons
- User needs to implement closeable or linkable notices
- User wants to create vertical scrolling notifications
- User asks about marquee-style text display

## Features

- **Horizontal Scroll**: Auto-scrolling text for long content
- **Vertical Scroll**: Support vertical scrolling with Swipe
- **Multiple Modes**: Closeable, link, and default modes
- **Custom Icons**: Left and right icon customization
- **Wrapable**: Text wrap support for multi-line display
- **Speed Control**: Configurable scroll speed
- **Custom Styling**: Full color and background customization

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| mode | Mode, can be set to `closeable` `link` | `string` | `''` |
| text | Notice text content | `string` | `''` |
| color | Text color | `string` | `#ed6a0c` |
| background | Background color | `string` | `#fffbe8` |
| left-icon | Left Icon | `string` | - |
| delay | Animation delay (s) | `number \| string` | `1` |
| speed | Scroll speed (px/s) | `number \| string` | `60` |
| scrollable | Whether to scroll content | `boolean` | - |
| wrapable | Whether to enable text wrap | `boolean` | `false` |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| click | Emitted when NoticeBar is clicked | `event: MouseEvent` |
| close | Emitted when NoticeBar is closed | `event: MouseEvent` |
| replay | Emitted when NoticeBar is replayed | - |

### Methods

| Name | Description | Attribute | Return value |
|------|-------------|-----------|--------------|
| reset | Reset NoticeBar | - | - |

### Slots

| Name | Description |
|------|-------------|
| default | Notice text content |
| left-icon | Custom left icon |
| right-icon | Custom right icon |

### Types

```ts
import type { NoticeBarMode, NoticeBarProps, NoticeBarInstance } from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-notice-bar
    text="Technology is the common soul of the people who developed it."
    left-icon="volume-o"
  />
</template>
```

### Scrollable

```vue
<template>
  <van-notice-bar scrollable text="Short Content" />
  
  <van-notice-bar
    :scrollable="false"
    text="Technology is the common soul of the people who developed it."
  />
</template>
```

### Wrapable

```vue
<template>
  <van-notice-bar wrapable :scrollable="false">
    Technology is the common soul of the people who developed it.
  </van-notice-bar>
</template>
```

### Closeable Mode

```vue
<template>
  <van-notice-bar mode="closeable">
    Short Content
  </van-notice-bar>
</template>
```

### Link Mode

```vue
<template>
  <van-notice-bar mode="link">
    Short Content
  </van-notice-bar>
</template>
```

### Custom Style

```vue
<template>
  <van-notice-bar color="#1989fa" background="#ecf9ff" left-icon="info-o">
    Short Content
  </van-notice-bar>
</template>
```

### Vertical Scroll

```vue
<template>
  <van-notice-bar left-icon="volume-o" :scrollable="false">
    <van-swipe
      vertical
      class="notice-swipe"
      :autoplay="3000"
      :touchable="false"
      :show-indicators="false"
    >
      <van-swipe-item>Content 1</van-swipe-item>
      <van-swipe-item>Content 2</van-swipe-item>
      <van-swipe-item>Content 3</van-swipe-item>
    </van-swipe>
  </van-notice-bar>
</template>

<style scoped>
.notice-swipe {
  height: 40px;
  line-height: 40px;
}
</style>
```

### Custom Icons

```vue
<template>
  <van-notice-bar>
    <template #left-icon>
      <van-icon name="volume-o" />
    </template>
    Custom left icon
  </van-notice-bar>
</template>
```

## Common Issues

### 1. Text Not Scrolling

Text only scrolls when it exceeds the container width. Force scrolling with `scrollable`:

```vue
<van-notice-bar scrollable text="Short text" />
```

### 2. Animation Delay

Default delay is 1 second. Adjust with `delay` prop:

```vue
<van-notice-bar :delay="0" text="Immediate start" />
```

### 3. Reset Animation

Use `reset` method to restart animation:

```vue
<template>
  <van-notice-bar ref="noticeBar" text="Content" />
  <van-button @click="noticeBar.reset()">Reset</van-button>
</template>
```

## Component Interactions

### With Dynamic Content

```vue
<template>
  <van-notice-bar
    v-if="notice"
    mode="closeable"
    :text="notice"
    @close="notice = ''"
  />
</template>

<script setup>
import { ref } from 'vue';

const notice = ref('Important announcement!');
</script>
```

### With Multiple Notices

```vue
<template>
  <van-notice-bar left-icon="volume-o" :scrollable="false">
    <van-swipe
      vertical
      :autoplay="3000"
      :show-indicators="false"
    >
      <van-swipe-item v-for="(item, index) in notices" :key="index">
        {{ item }}
      </van-swipe-item>
    </van-swipe>
  </van-notice-bar>
</template>

<script setup>
import { ref } from 'vue';

const notices = ref([
  'Notice 1',
  'Notice 2',
  'Notice 3',
]);
</script>
```

### With Navigation

```vue
<template>
  <van-notice-bar
    mode="link"
    @click="goToDetail"
  >
    Click to view details
  </van-notice-bar>
</template>

<script setup>
import { useRouter } from 'vue-router';

const router = useRouter();

const goToDetail = () => {
  router.push('/detail');
};
</script>
```

## Best Practices

1. **Use appropriate mode**: Choose closeable or link mode based on use case
2. **Keep messages concise**: Short messages are more effective
3. **Use icons wisely**: Add icons for better visual recognition
4. **Consider accessibility**: Ensure notices are accessible to all users
5. **Test scrolling**: Verify scrolling behavior on different screen sizes
