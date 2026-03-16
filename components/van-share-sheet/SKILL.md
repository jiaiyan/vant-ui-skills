---
name: "van-share-sheet"
description: "Share sheet component for displaying sharing options panel. Invoke when user needs to implement share functionality, social sharing menus, or content distribution interfaces."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant ShareSheet Component

A bottom sharing panel for displaying action buttons corresponding to each sharing channel.

## When to Invoke

Invoke this skill when:
- User needs to implement share functionality
- User wants to display social sharing options
- User needs to create a share menu with multiple platforms
- User asks about implementing share sheets
- User wants custom share icons and options

## Features

- **Built-in Icons**: WeChat, Weibo, QQ, Link, QR code, etc.
- **Multi-line Layout**: Support multiple rows of options
- **Custom Icons**: Support custom icon URLs
- **Description**: Optional description text
- **Cancel Button**: Built-in cancel option
- **Safe Area**: Bottom safe area adaptation

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model:show | Whether to show ShareSheet | `boolean` | `false` |
| options | Share options | `Option[]` | `[]` |
| title | Title | `string` | - |
| cancel-text | Cancel button text | `string` | `'Cancel'` |
| description | Description | `string` | - |
| duration | Transition duration, unit second | `number \| string` | `0.3` |
| z-index | z-index | `number \| string` | `2000+` |
| round | Whether to show round corner | `boolean` | `true` |
| overlay | Whether to show overlay | `boolean` | `true` |
| overlay-class | Custom overlay class | `string \| Array \| object` | - |
| overlay-style | Custom overlay style | `object` | - |
| lock-scroll | Whether to lock background scroll | `boolean` | `true` |
| lazy-render | Whether to lazy render until appeared | `boolean` | `true` |
| close-on-popstate | Whether to close when popstate | `boolean` | `true` |
| close-on-click-overlay | Whether to close when overlay is clicked | `boolean` | `true` |
| safe-area-inset-bottom | Enable bottom safe area adaptation | `boolean` | `true` |
| teleport | Target element for mounting | `string \| Element` | - |
| before-close | Callback before close | `(action: string) => boolean \| Promise<boolean>` | - |

### Option Data Structure

| Key | Description | Type |
|-----|-------------|------|
| name | Option name | `string` |
| description | Option description | `string` |
| icon | Icon name or URL | `string` |
| className | Option className | `string` |

### Built-in Icons

- `wechat` - WeChat
- `wechat-moments` - WeChat Moments
- `weibo` - Weibo
- `qq` - QQ
- `link` - Link
- `qrcode` - QR Code
- `poster` - Poster
- `weapp-qrcode` - Mini Program QR Code

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| select | Emitted when an option is clicked | `option: Option, index: number` |
| cancel | Emitted when cancel button is clicked | - |
| open | Emitted when opening ShareSheet | - |
| close | Emitted when closing ShareSheet | - |
| opened | Emitted when ShareSheet is opened | - |
| closed | Emitted when ShareSheet is closed | - |
| click-overlay | Emitted when overlay is clicked | `event: MouseEvent` |

### Slots

| Name | Description |
|------|-------------|
| title | Custom title |
| description | Custom description |
| cancel | Custom cancel button content |

### Types

```ts
import type { ShareSheetProps, ShareSheetOption, ShareSheetOptions } from 'vant'
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-cell title="Show ShareSheet" @click="showShare = true" />
  <van-share-sheet
    v-model:show="showShare"
    title="Share"
    :options="options"
    @select="onSelect"
  />
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const showShare = ref(false)
const options = [
  { name: 'WeChat', icon: 'wechat' },
  { name: 'Weibo', icon: 'weibo' },
  { name: 'Link', icon: 'link' },
  { name: 'Poster', icon: 'poster' },
  { name: 'QRCode', icon: 'qrcode' }
]

const onSelect = (option) => {
  showToast(option.name)
  showShare.value = false
}
</script>
```

### Multi-line Layout

```vue
<template>
  <van-share-sheet v-model:show="showShare" title="Share" :options="options" />
</template>

<script setup>
import { ref } from 'vue'

const showShare = ref(false)
const options = [
  [
    { name: 'WeChat', icon: 'wechat' },
    { name: 'Moments', icon: 'wechat-moments' },
    { name: 'Weibo', icon: 'weibo' },
    { name: 'QQ', icon: 'qq' }
  ],
  [
    { name: 'Link', icon: 'link' },
    { name: 'Poster', icon: 'poster' },
    { name: 'QRCode', icon: 'qrcode' },
    { name: 'Mini Program', icon: 'weapp-qrcode' }
  ]
]
</script>
```

### Custom Icons

```vue
<template>
  <van-share-sheet v-model:show="showShare" :options="options" />
</template>

<script setup>
import { ref } from 'vue'

const showShare = ref(false)
const options = [
  {
    name: 'Custom 1',
    icon: 'https://fastly.jsdelivr.net/npm/@vant/assets/custom-icon-fire.png'
  },
  {
    name: 'Custom 2',
    icon: 'https://fastly.jsdelivr.net/npm/@vant/assets/custom-icon-light.png'
  },
  {
    name: 'Custom 3',
    icon: 'https://fastly.jsdelivr.net/npm/@vant/assets/custom-icon-water.png'
  }
]
</script>
```

### With Description

```vue
<template>
  <van-share-sheet
    v-model:show="showShare"
    :options="options"
    title="Share"
    description="Share to your friends"
  />
</template>

<script setup>
import { ref } from 'vue'

const showShare = ref(false)
const options = [
  { name: 'WeChat', icon: 'wechat' },
  { name: 'Weibo', icon: 'weibo' },
  { name: 'Link', icon: 'link', description: 'Copy link' }
]
</script>
```

## Common Issues

### 1. ShareSheet Not Closing

Handle the `select` event to close:

```vue
<van-share-sheet 
  v-model:show="showShare" 
  :options="options" 
  @select="onSelect"
/>

<script setup>
const onSelect = (option) => {
  handleShare(option)
  showShare.value = false
}
</script>
```

### 2. Custom Share Logic

Implement share logic in select handler:

```vue
<script setup>
const onSelect = (option) => {
  switch (option.name) {
    case 'WeChat':
      shareToWeChat()
      break
    case 'Link':
      copyToClipboard(shareUrl)
      break
    case 'QRCode':
      showQRCode()
      break
  }
  showShare.value = false
}
</script>
```

### 3. Disable Cancel Button

Set `cancel-text` to empty:

```vue
<van-share-sheet v-model:show="showShare" :options="options" cancel-text="" />
```

## Component Interactions

### With Copy Link

```vue
<script setup>
import { showToast } from 'vant'

const onSelect = async (option) => {
  if (option.icon === 'link') {
    await navigator.clipboard.writeText(shareUrl)
    showToast('Link copied')
  }
  showShare.value = false
}
</script>
```

### With QR Code Display

```vue
<template>
  <van-share-sheet v-model:show="showShare" :options="options" @select="onSelect" />
  <van-dialog v-model:show="showQRCode" title="QR Code">
    <img :src="qrCodeUrl" />
  </van-dialog>
</template>

<script setup>
import { ref } from 'vue'

const showShare = ref(false)
const showQRCode = ref(false)

const options = [
  { name: 'WeChat', icon: 'wechat' },
  { name: 'QRCode', icon: 'qrcode' }
]

const onSelect = (option) => {
  if (option.icon === 'qrcode') {
    showQRCode.value = true
  }
  showShare.value = false
}
</script>
```

### With Article Sharing

```vue
<template>
  <van-cell-group>
    <van-cell title="Share Article" @click="showShare = true" />
  </van-cell-group>
  
  <van-share-sheet
    v-model:show="showShare"
    title="Share Article"
    :description="article.title"
    :options="shareOptions"
    @select="handleShare"
  />
</template>

<script setup>
import { ref } from 'vue'

const article = ref({
  title: 'Article Title',
  url: 'https://example.com/article/1'
})

const showShare = ref(false)
const shareOptions = [
  { name: 'WeChat', icon: 'wechat' },
  { name: 'Moments', icon: 'wechat-moments' },
  { name: 'Link', icon: 'link' }
]

const handleShare = (option) => {
  // Implement actual share logic
  showShare.value = false
}
</script>
```

## Best Practices

1. **Group options**: Use multi-line layout for many options
2. **Clear naming**: Use descriptive names for share options
3. **Platform icons**: Use built-in icons for common platforms
4. **Description**: Add description for context
5. **Handle errors**: Provide feedback if share fails
6. **Accessibility**: Ensure options are accessible
