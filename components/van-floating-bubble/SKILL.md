---
name: "van-floating-bubble"
description: "Floating bubble component for creating draggable floating buttons. Invoke when user needs to implement floating action buttons, draggable help buttons, or always-visible interactive elements."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant FloatingBubble Component

A clickable bubble that hovers around the edge of the page, supporting drag interactions and magnetic吸附 (snap to edge) behavior.

## When to Invoke

Invoke this skill when:
- User needs to implement a floating action button
- User wants a draggable help or support button
- User needs an always-visible interactive element
- User asks about implementing floating chat buttons
- User wants magnetic snap-to-edge functionality

## Features

- **Draggable**: Support free or axis-constrained dragging
- **Magnetic Snap**: Auto-snap to screen edges
- **Position Control**: Control position via v-model
- **Custom Icon**: Configurable icon display
- **Gap Control**: Minimum gap from window edges
- **Teleport**: Mount to specified element

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model:offset | Control bubble position | `OffsetType` | Default right-bottom coordinate |
| axis | Drag direction: `x`, `y`, `xy`, `lock` | `'x' \| 'y' \| 'xy' \| 'lock'` | `y` |
| magnetic | Direction of automatic magnetic absorption | `'x' \| 'y'` | - |
| icon | Bubble icon | `string` | - |
| gap | Minimum gap between bubble and window | `number \| { x: number, y: number }` | `24` |
| teleport | Target element for mounting | `string \| Element` | `body` |

### OffsetType

```ts
interface OffsetType {
  x: number
  y: number
}
```

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| click | Triggered when component is clicked | `MouseEvent` |
| offset-change | Triggered when position changes by dragging | `{ x: number, y: number }` |

### Slots

| Name | Description |
|------|-------------|
| default | Customize the bubble display content |

### Types

```ts
import type {
  FloatingBubbleProps,
  FloatingBubbleAxis,
  FloatingBubbleMagnetic,
  FloatingBubbleOffset
} from 'vant'
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-floating-bubble icon="chat" @click="onClick" />
</template>

<script setup>
import { showToast } from 'vant'

const onClick = () => {
  showToast('Click Bubble')
}
</script>
```

### Free Drag with Magnetic Snap

```vue
<template>
  <van-floating-bubble
    axis="xy"
    icon="chat"
    magnetic="x"
    @offset-change="onOffsetChange"
  />
</template>

<script setup>
import { showToast } from 'vant'

const onOffsetChange = (offset) => {
  showToast(`x: ${offset.x.toFixed(0)}, y: ${offset.y.toFixed(0)}`)
}
</script>
```

### Controlled Position

```vue
<template>
  <van-floating-bubble v-model:offset="offset" axis="xy" icon="chat" />
  <van-button @click="resetPosition">Reset Position</van-button>
</template>

<script setup>
import { ref } from 'vue'

const offset = ref({ x: 200, y: 400 })

const resetPosition = () => {
  offset.value = { x: 200, y: 400 }
}
</script>
```

### Custom Content

```vue
<template>
  <van-floating-bubble axis="xy" magnetic="x">
    <van-icon name="service" size="24" />
  </van-floating-bubble>
</template>
```

### Lock Position

```vue
<template>
  <van-floating-bubble axis="lock" icon="chat" />
</template>
```

## Common Issues

### 1. Bubble Position Reset on Scroll

The bubble uses fixed positioning and should stay in place. If issues occur, check for CSS transforms on parent elements.

### 2. Custom Gap Configuration

Set different gaps for x and y axes:

```vue
<van-floating-bubble :gap="{ x: 16, y: 32 }" />
```

### 3. Preventing Click During Drag

The click event fires after drag ends. Check offset-change to determine if dragging occurred:

```vue
<script setup>
const isDragging = ref(false)

const onOffsetChange = () => {
  isDragging.value = true
}

const onClick = () => {
  if (!isDragging.value) {
    console.log('Real click')
  }
  isDragging.value = false
}
</script>
```

## Component Interactions

### With Customer Service Chat

```vue
<template>
  <van-floating-bubble 
    icon="service" 
    @click="openChat"
  />
  
  <van-popup v-model:show="showChat" position="bottom" :style="{ height: '60%' }">
    <chat-window />
  </van-popup>
</template>

<script setup>
import { ref } from 'vue'

const showChat = ref(false)

const openChat = () => {
  showChat.value = true
}
</script>
```

### With Back to Top

```vue
<template>
  <van-floating-bubble 
    v-model:offset="offset"
    axis="y"
    @click="scrollToTop"
  >
    <van-icon name="back-top" size="24" />
  </van-floating-bubble>
</template>

<script setup>
const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}
</script>
```

### With Quick Actions Menu

```vue
<template>
  <van-floating-bubble icon="plus" @click="showActions = true" />
  
  <van-action-sheet v-model:show="showActions" :actions="actions" />
</template>

<script setup>
import { ref } from 'vue'

const showActions = ref(false)
const actions = [
  { name: 'New Post', icon: 'edit' },
  { name: 'Upload', icon: 'photo' },
  { name: 'Share', icon: 'share' }
]
</script>
```

## Best Practices

1. **Position persistence**: Save position to localStorage for returning users
2. **Magnetic snap**: Use `magnetic="x"` for better mobile UX
3. **Touch targets**: Ensure bubble is large enough for touch (48px default)
4. **Visual feedback**: Provide clear visual state on interaction
5. **Avoid blocking**: Position bubble to avoid blocking important content
6. **Accessibility**: Add aria-label for screen readers
