---
name: "van-icon"
description: "Icon component based on font icons. Invoke when user needs to display icons, badges on icons, custom icon fonts, or use icons in other components."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Icon Component

Font-based icon component with badge support and customization capabilities.

## When to Invoke

Invoke this skill when:
- User needs to display icons in the UI
- User wants to show badges or dots on icons
- User needs to customize icon colors or sizes
- User wants to use custom icon fonts
- User asks about icon URLs or image icons
- User needs clickable icons
- User wants to use icons in other components

## Features

- **Built-in Icons**: 100+ built-in icons
- **Image Support**: Use image URLs as icons
- **Badge Support**: Show dot or badge on icons
- **Custom Colors**: Set icon color directly
- **Custom Sizes**: Flexible size configuration
- **Custom Icon Font**: Support for custom icon fonts
- **Clickable**: Support click events
- **Badge Props**: Pass props to badge component

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| name | Icon name or URL | `string` | `''` |
| dot | Whether to show red dot | `boolean` | `false` |
| badge | Content of the badge | `number \| string` | `''` |
| badge-props | Props of Badge component | `BadgeProps` | - |
| color | Icon color | `string` | `inherit` |
| size | Icon size | `number \| string` | `inherit` |
| class-prefix | ClassName prefix | `string` | `van-icon` |
| tag | HTML tag of root element | `string` | `i` |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| click | Emitted when icon is clicked | `event: MouseEvent` |

### Types

```ts
import type { IconProps } from 'vant';
```

### CSS Variables

| Name | Default Value | Description |
|------|---------------|-------------|
| --van-icon-font-family | `'van-icon'` | Icon font family |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-icon name="chat-o" />
</template>
```

### Using Image URL

```vue
<template>
  <van-icon name="https://fastly.jsdelivr.net/npm/@vant/assets/icon-demo.png" />
</template>
```

### Show Badge

```vue
<template>
  <div class="icon-demo">
    <van-icon name="chat-o" dot />
    <van-icon name="chat-o" badge="9" />
    <van-icon name="chat-o" badge="99+" />
  </div>
</template>
```

### Icon Color

```vue
<template>
  <div class="icon-demo">
    <van-icon name="cart-o" color="#1989fa" />
    <van-icon name="fire-o" color="#ee0a24" />
    <van-icon name="star-o" color="#ff976a" />
  </div>
</template>
```

### Icon Size

```vue
<template>
  <div class="icon-demo">
    <!-- Using px unit by default -->
    <van-icon name="chat-o" size="40" />
    <!-- Using rem unit -->
    <van-icon name="chat-o" size="3rem" />
    <!-- Using string -->
    <van-icon name="chat-o" size="40px" />
  </div>
</template>
```

### Clickable Icon

```vue
<template>
  <van-icon name="setting-o" @click="handleClick" />
</template>

<script setup>
const handleClick = () => {
  console.log('Icon clicked')
}
</script>
```

### Custom Icon Font

```vue
<template>
  <van-icon class-prefix="my-icon" name="extra" />
</template>

<style>
@font-face {
  font-family: 'my-icon';
  src: url('./my-icon.ttf') format('truetype');
}

.my-icon {
  font-family: 'my-icon';
}

.my-icon-extra::before {
  content: '\e626';
}
</style>
```

### Badge with Props

```vue
<template>
  <van-icon
    name="chat-o"
    badge="5"
    :badge-props="{ color: '#1989fa' }"
  />
</template>
```

### Icon Grid

```vue
<template>
  <van-grid :column-num="4">
    <van-grid-item
      v-for="icon in icons"
      :key="icon"
      :icon="icon"
      :text="icon"
    />
  </van-grid>
</template>

<script setup>
const icons = [
  'chat-o',
  'friends-o',
  'setting-o',
  'location-o',
  'star-o',
  'like-o',
  'gold-coin-o',
  'info-o',
]
</script>
```

### Icon in Tabbar

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
import { ref } from 'vue'

const active = ref(0)
</script>
```

### Icon in NavBar

```vue
<template>
  <van-nav-bar title="Title">
    <template #left>
      <van-icon name="arrow-left" @click="goBack" />
    </template>
    <template #right>
      <van-icon name="search" @click="search" />
    </template>
  </van-nav-bar>
</template>

<script setup>
const goBack = () => {
  console.log('Go back')
}

const search = () => {
  console.log('Search')
}
</script>
```

### Icon in Cell

```vue
<template>
  <van-cell-group>
    <van-cell title="Location" icon="location-o" is-link />
    <van-cell title="Settings" icon="setting-o" is-link />
    <van-cell title="User" icon="user-o" is-link />
  </van-cell-group>
</template>
```

### Icon in Button

```vue
<template>
  <div class="button-demo">
    <van-button icon="plus" type="primary" />
    <van-button icon="plus" type="primary">Button</van-button>
    <van-button icon="success" type="success">Success</van-button>
  </div>
</template>
```

### Icon with Loading

```vue
<template>
  <van-icon :name="loading ? 'replay' : 'success'" :class="{ 'van-icon-spin': loading }" />
</template>

<script setup>
import { ref } from 'vue'

const loading = ref(false)
</script>

<style scoped>
.van-icon-spin {
  animation: spin 1s linear infinite;
}

@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
</style>
```

### Social Media Icons

```vue
<template>
  <div class="social-icons">
    <van-icon name="wechat" size="32" color="#07c160" />
    <van-icon name="alipay" size="32" color="#1677ff" />
    <van-icon name="weibo" size="32" color="#ee0a24" />
  </div>
</template>

<style scoped>
.social-icons {
  display: flex;
  gap: 16px;
}
</style>
```

## Built-in Icons

Vant provides 100+ built-in icons. Here are some commonly used ones:

### Basic Icons

- `success` - Success
- `cross` - Close
- `plus` - Add
- `minus` - Minus
- `info-o` - Info outline
- `warning-o` - Warning outline
- `question-o` - Question outline

### Navigation Icons

- `arrow-left` - Left arrow
- `arrow-up` - Up arrow
- `arrow-down` - Down arrow
- `arrow` - Right arrow
- `location-o` - Location outline
- `guide-o` - Guide outline

### User Icons

- `user-o` - User outline
- `friends-o` - Friends outline
- `contact` - Contact
- `manager-o` - Manager outline

### Action Icons

- `edit` - Edit
- `delete` - Delete
- `search` - Search
- `setting-o` - Settings outline
- `share` - Share
- `star-o` - Star outline
- `like-o` - Like outline

### Media Icons

- `photo-o` - Photo outline
- `video-o` - Video outline
- `music-o` - Music outline
- `volume-o` - Volume outline

### E-commerce Icons

- `cart-o` - Cart outline
- `shop-o` - Shop outline
- `gold-coin-o` - Gold coin outline
- `gift-o` - Gift outline

### Communication Icons

- `chat-o` - Chat outline
- `comment-o` - Comment outline
- `phone-o` - Phone outline
- `envelop-o` - Email outline

## Common Issues

### 1. Icon Not Displaying

Make sure the icon name is correct:

```vue
<!-- Correct -->
<van-icon name="chat-o" />

<!-- Incorrect (no such icon) -->
<van-icon name="chat-outline" />
```

### 2. Custom Icon Font Not Working

Ensure the font-family is correctly set:

```css
.my-icon {
  font-family: 'my-icon' !important;
}
```

### 3. Icon Size Inheritance

When size is not set, icon inherits from parent:

```vue
<div style="font-size: 24px">
  <van-icon name="chat-o" /> <!-- Will be 24px -->
</div>
```

## Component Interactions

### With Badge

```vue
<template>
  <van-icon name="chat-o" :badge="unreadCount" />
</template>

<script setup>
import { ref } from 'vue'

const unreadCount = ref(5)
</script>
```

### With Popup

```vue
<template>
  <van-icon name="info-o" @click="showInfo = true" />
  <van-popup v-model:show="showInfo">
    <div class="info-content">Information</div>
  </van-popup>
</template>

<script setup>
import { ref } from 'vue'

const showInfo = ref(false)
</script>
```

### With Toast

```vue
<template>
  <van-icon name="success" @click="showToast" />
</template>

<script setup>
import { showToast } from 'vant'

const showToast = () => {
  showToast('Success!')
}
</script>
```

## Best Practices

1. **Use semantic icons**: Choose icons that match the action or content
2. **Consistent sizing**: Use consistent icon sizes within the same context
3. **Accessible labels**: Add aria-label for icon-only buttons
4. **Color contrast**: Ensure sufficient contrast for visibility
5. **Touch targets**: Make clickable icons large enough for touch (minimum 44px)
6. **Badge usage**: Use badges sparingly to avoid visual clutter
7. **Custom icons**: Use custom icon fonts for brand-specific icons
8. **Performance**: Use font icons instead of images for better performance
