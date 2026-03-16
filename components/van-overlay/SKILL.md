---
name: "van-overlay"
description: "Overlay component for creating modal mask layers. Invoke when user needs to implement modal overlays, loading masks, or prevent user interactions during operations."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Overlay Component

A mask layer component used to emphasize specific page elements and prevent users from performing other operations.

## When to Invoke

Invoke this skill when:
- User needs to create a modal overlay/mask
- User wants to prevent user interactions during operations
- User needs to display content over a dimmed background
- User asks about implementing loading overlays
- User wants to create custom modal backgrounds

## Features

- **Simple API**: Easy to use with show prop
- **Custom Styling**: Configurable z-index and animation
- **Content Embedding**: Support any content via slots
- **Scroll Lock**: Optional background scroll locking
- **Lazy Render**: Performance optimization option
- **Teleport**: Mount to specified element

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| show | Whether to show overlay | `boolean` | `false` |
| z-index | z-index | `number \| string` | `1` |
| duration | Animation duration | `number \| string` | `0.3` |
| class-name | ClassName | `string` | - |
| custom-class | Custom style | `object` | - |
| lock-scroll | Whether to lock background scroll | `boolean` | `true` |
| lazy-render | Whether to lazy render until appeared | `boolean` | `true` |
| teleport | Target element for mounting | `string \| Element` | - |

### Events

| Event | Description | Parameters |
|-------|-------------|------------|
| click | Emitted when component is clicked | `event: MouseEvent` |

### Slots

| Name | Description |
|------|-------------|
| default | Default slot for embedded content |

### Types

```ts
import type { OverlayProps } from 'vant'
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-button type="primary" @click="show = true">Show Overlay</van-button>
  <van-overlay :show="show" @click="show = false" />
</template>

<script setup>
import { ref } from 'vue'

const show = ref(false)
</script>
```

### Embedded Content

```vue
<template>
  <van-overlay :show="show" @click="show = false">
    <div class="wrapper" @click.stop>
      <div class="block" />
    </div>
  </van-overlay>
</template>

<script setup>
import { ref } from 'vue'

const show = ref(false)
</script>

<style scoped>
.wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
}

.block {
  width: 120px;
  height: 120px;
  background-color: #fff;
}
</style>
```

### Custom z-index

```vue
<template>
  <van-overlay :show="show" z-index="100" />
</template>
```

### Loading Overlay

```vue
<template>
  <van-overlay :show="loading" class-name="loading-overlay">
    <div class="loading-wrapper">
      <van-loading type="spinner" color="#fff" />
    </div>
  </van-overlay>
</template>

<script setup>
import { ref } from 'vue'

const loading = ref(false)
</script>

<style scoped>
.loading-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}
</style>
```

### Custom Animation Duration

```vue
<template>
  <van-overlay :show="show" :duration="0.5" />
</template>
```

## Common Issues

### 1. Content Click Closes Overlay

Use `@click.stop` on content to prevent propagation:

```vue
<van-overlay :show="show" @click="show = false">
  <div class="content" @click.stop>
    <!-- Content won't trigger close -->
  </div>
</van-overlay>
```

### 2. Overlay Behind Other Elements

Increase z-index:

```vue
<van-overlay :show="show" z-index="2000" />
```

### 3. Scroll Not Locked

Ensure `lock-scroll` is `true` (default):

```vue
<van-overlay :show="show" lock-scroll />
```

### 4. Custom Background Color

Use custom-style:

```vue
<van-overlay 
  :show="show" 
  :custom-style="{ background: 'rgba(0, 0, 0, 0.8)' }" 
/>
```

## Component Interactions

### With Loading State

```vue
<template>
  <van-overlay :show="loading">
    <div class="loading-wrapper">
      <van-loading vertical color="#fff">Loading...</van-loading>
    </div>
  </van-overlay>
</template>

<script setup>
import { ref } from 'vue'

const loading = ref(false)

const fetchData = async () => {
  loading.value = true
  try {
    await apiCall()
  } finally {
    loading.value = false
  }
}
</script>
```

### With Custom Modal

```vue
<template>
  <van-overlay :show="show" @click="closeModal">
    <div class="modal-wrapper" @click.stop>
      <div class="modal">
        <h3>Modal Title</h3>
        <p>Modal content here</p>
        <van-button type="primary" @click="closeModal">Close</van-button>
      </div>
    </div>
  </van-overlay>
</template>

<script setup>
import { ref } from 'vue'

const show = ref(false)

const closeModal = () => {
  show.value = false
}
</script>

<style scoped>
.modal-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}

.modal {
  background: #fff;
  padding: 20px;
  border-radius: 8px;
  width: 80%;
  max-width: 320px;
}
</style>
```

### With Image Preview

```vue
<template>
  <van-overlay :show="show" @click="show = false">
    <div class="image-preview" @click.stop>
      <img :src="currentImage" />
    </div>
  </van-overlay>
</template>

<style scoped>
.image-preview {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}

.image-preview img {
  max-width: 90%;
  max-height: 90%;
}
</style>
```

## Best Practices

1. **Click handling**: Use `@click.stop` on content to prevent unwanted closes
2. **z-index management**: Coordinate z-index with other overlays
3. **Accessibility**: Add aria-hidden when overlay is not visible
4. **Performance**: Use lazy-render for complex content
5. **Animation**: Match duration with other UI elements
6. **Scroll lock**: Keep enabled for modal-like behavior
