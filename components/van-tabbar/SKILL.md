---
name: "van-tabbar"
description: "Tabbar component for bottom navigation between pages. Invoke when user needs to implement bottom navigation bar for main app navigation."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Tabbar Component

Tabbar component used to switch between different pages, commonly used as the main navigation for mobile applications.

## When to Invoke

Invoke this skill when:
- User needs to implement bottom navigation bar
- User wants to switch between main app pages
- User needs to show badges on navigation items
- User wants to customize tabbar icons and colors
- User asks about route mode or fixed positioning

## Features

- **Bottom Navigation**: Fixed at bottom for easy access
- **Icon Support**: Display icons with text labels
- **Badge Support**: Show dot or number badges
- **Custom Icons**: Use custom images for icons
- **Route Mode**: Integrate with Vue Router
- **Custom Colors**: Customize active and inactive colors
- **Safe Area**: Support bottom safe area adaptation
- **Before Change**: Validate before switching tabs

## API Reference

### Tabbar Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model | Identifier of current tab | `number \| string` | `0` |
| fixed | Whether to fix at bottom | `boolean` | `true` |
| border | Whether to show border | `boolean` | `true` |
| z-index | Z-index level | `number \| string` | `1` |
| active-color | Color of active tab | `string` | `#1989fa` |
| inactive-color | Color of inactive tab | `string` | `#7d7e80` |
| route | Whether to enable route mode | `boolean` | `false` |
| placeholder | Whether to generate placeholder | `boolean` | `false` |
| safe-area-inset-bottom | Whether to enable safe area | `boolean` | `false` |
| before-change | Callback before changing tab | `(name) => boolean \| Promise<boolean>` | - |

### Tabbar Events

| Name | Description | Arguments |
|------|-------------|-----------|
| change | Emitted when active tab changes | `active: number \| string` |

### TabbarItem Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| name | Item identifier | `number \| string` | Item index |
| icon | Icon name | `string` | - |
| icon-prefix | Icon className prefix | `string` | `van-icon` |
| dot | Whether to show red dot | `boolean` | - |
| badge | Badge content | `number \| string` | `''` |
| badge-props | Props of Badge component | `BadgeProps` | - |
| url | Link URL | `string` | - |
| to | Target route object | `string \| object` | - |
| replace | Whether to replace history | `boolean` | `false` |

### TabbarItem Slots

| Name | Description | SlotProps |
|------|-------------|-----------|
| icon | Custom icon | `active: boolean` |

### Types

```ts
import type { TabbarProps, TabbarItemProps } from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-tabbar v-model="active">
    <van-tabbar-item icon="home-o">Home</van-tabbar-item>
    <van-tabbar-item icon="search">Search</van-tabbar-item>
    <van-tabbar-item icon="friends-o">Friends</van-tabbar-item>
    <van-tabbar-item icon="setting-o">Settings</van-tabbar-item>
  </van-tabbar>
</template>

<script setup>
import { ref } from 'vue';

const active = ref(0);
</script>
```

### Match By Name

```vue
<template>
  <van-tabbar v-model="active">
    <van-tabbar-item name="home" icon="home-o">Home</van-tabbar-item>
    <van-tabbar-item name="search" icon="search">Search</van-tabbar-item>
    <van-tabbar-item name="friends" icon="friends-o">Friends</van-tabbar-item>
    <van-tabbar-item name="settings" icon="setting-o">Settings</van-tabbar-item>
  </van-tabbar>
</template>

<script setup>
import { ref } from 'vue';

const active = ref('home');
</script>
```

### Show Badge

```vue
<template>
  <van-tabbar v-model="active">
    <van-tabbar-item icon="home-o">Home</van-tabbar-item>
    <van-tabbar-item icon="search" dot>Search</van-tabbar-item>
    <van-tabbar-item icon="friends-o" badge="5">Friends</van-tabbar-item>
    <van-tabbar-item icon="setting-o" badge="20">Settings</van-tabbar-item>
  </van-tabbar>
</template>

<script setup>
import { ref } from 'vue';

const active = ref(0);
</script>
```

### Custom Icon

```vue
<template>
  <van-tabbar v-model="active">
    <van-tabbar-item badge="3">
      <span>Custom</span>
      <template #icon="props">
        <img :src="props.active ? icon.active : icon.inactive" />
      </template>
    </van-tabbar-item>
    <van-tabbar-item icon="search">Search</van-tabbar-item>
    <van-tabbar-item icon="setting-o">Settings</van-tabbar-item>
  </van-tabbar>
</template>

<script setup>
import { ref } from 'vue';

const active = ref(0);
const icon = {
  active: 'https://fastly.jsdelivr.net/npm/@vant/assets/user-active.png',
  inactive: 'https://fastly.jsdelivr.net/npm/@vant/assets/user-inactive.png',
};
</script>
```

### Custom Color

```vue
<template>
  <van-tabbar v-model="active" active-color="#ee0a24">
    <van-tabbar-item icon="home-o">Home</van-tabbar-item>
    <van-tabbar-item icon="search">Search</van-tabbar-item>
    <van-tabbar-item icon="friends-o">Friends</van-tabbar-item>
    <van-tabbar-item icon="setting-o">Settings</van-tabbar-item>
  </van-tabbar>
</template>

<script setup>
import { ref } from 'vue';

const active = ref(0);
</script>
```

### Route Mode

```vue
<template>
  <router-view />
  <van-tabbar route>
    <van-tabbar-item replace to="/home" icon="home-o">Home</van-tabbar-item>
    <van-tabbar-item replace to="/search" icon="search">Search</van-tabbar-item>
  </van-tabbar>
</template>
```

### With Change Event

```vue
<template>
  <van-tabbar v-model="active" @change="onChange">
    <van-tabbar-item icon="home-o">Home</van-tabbar-item>
    <van-tabbar-item icon="search">Search</van-tabbar-item>
    <van-tabbar-item icon="friends-o">Friends</van-tabbar-item>
    <van-tabbar-item icon="setting-o">Settings</van-tabbar-item>
  </van-tabbar>
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const active = ref(0);

const onChange = (index) => {
  showToast(`Tab ${index}`);
};
</script>
```

### With Placeholder

```vue
<template>
  <van-tabbar v-model="active" fixed placeholder>
    <van-tabbar-item icon="home-o">Home</van-tabbar-item>
    <van-tabbar-item icon="search">Search</van-tabbar-item>
  </van-tabbar>
</template>

<script setup>
import { ref } from 'vue';

const active = ref(0);
</script>
```

## Best Practices

1. **Use route mode**: Integrate with Vue Router for page navigation
2. **Limit items**: Keep 3-5 items for better usability
3. **Use badges wisely**: Show badges only for items requiring attention
4. **Custom colors**: Match active color with your brand
5. **Safe area**: Enable safe area for iOS devices
6. **Placeholder**: Use placeholder to prevent content overlap
