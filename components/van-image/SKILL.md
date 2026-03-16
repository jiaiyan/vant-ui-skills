---
name: "van-image"
description: "Enhanced image component with multiple fill modes, lazy loading, and placeholder support. Invoke when user needs to display images with custom fit modes, lazy loading, or loading/error states."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Image Component

Enhanced img tag with multiple image fill modes, lazy loading, and placeholder support.

## When to Invoke

Invoke this skill when:
- User needs to display images with custom fit modes
- User wants to implement lazy loading for images
- User needs loading or error placeholders
- User wants to create round or rounded images
- User asks about image positioning
- User needs responsive images
- User wants to handle image load events

## Features

- **Multiple Fit Modes**: contain, cover, fill, none, scale-down
- **Lazy Loading**: Built-in lazy loading support
- **Loading Placeholder**: Custom loading state
- **Error Placeholder**: Custom error state
- **Round Shape**: Round image support
- **Border Radius**: Custom border radius
- **Position Control**: Image position customization
- **Event Handling**: Load and error events
- **Block Mode**: Block-level element option

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| src | Image source URL | `string` | - |
| fit | Fit mode, same as object-fit | `string` | `fill` |
| position | Position, same as object-position | `string` | `center` |
| alt | Alt text | `string` | - |
| width | Width | `number \| string` | - |
| height | Height | `number \| string` | - |
| radius | Border radius | `number \| string` | `0` |
| round | Whether to be round | `boolean` | `false` |
| block | Whether the root node is a block element | `boolean` | `false` |
| lazy-load | Whether to enable lazy load | `boolean` | `false` |
| show-error | Whether to show error placeholder | `boolean` | `true` |
| show-loading | Whether to show loading placeholder | `boolean` | `true` |
| error-icon | Error icon | `string` | `photo-fail` |
| loading-icon | Loading icon | `string` | `photo` |
| icon-size | Icon size | `number \| string` | `32px` |
| icon-prefix | Icon className prefix | `string` | `van-icon` |
| crossorigin | CORS setting | `string` | - |
| referrerpolicy | Referrer policy | `string` | - |
| decoding | Decoding hint | `string` | - |

### Fit Modes

| Name | Description |
|------|-------------|
| contain | Keep aspect ratio, fully display the long side of the image |
| cover | Keep aspect ratio, fully display the short side of the image, cutting the long side |
| fill | Stretch and resize image to fill the content box |
| none | Not resize image |
| scale-down | Take the smaller of `none` or `contain` |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| click | Emitted when image is clicked | `event: MouseEvent` |
| load | Emitted when image loaded | `event: Event` |
| error | Emitted when image load failed | - |

### Slots

| Name | Description |
|------|-------------|
| default | Custom the content below the image |
| loading | Custom loading placeholder |
| error | Custom error placeholder |

### Types

```ts
import type { ImageFit, ImagePosition, ImageProps } from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-image
    width="100"
    height="100"
    src="https://fastly.jsdelivr.net/npm/@vant/assets/cat.jpeg"
  />
</template>
```

### Fit Mode

```vue
<template>
  <div class="image-demo">
    <van-image
      width="10rem"
      height="10rem"
      fit="contain"
      src="https://fastly.jsdelivr.net/npm/@vant/assets/cat.jpeg"
    />
    <van-image
      width="10rem"
      height="10rem"
      fit="cover"
      src="https://fastly.jsdelivr.net/npm/@vant/assets/cat.jpeg"
    />
    <van-image
      width="10rem"
      height="10rem"
      fit="fill"
      src="https://fastly.jsdelivr.net/npm/@vant/assets/cat.jpeg"
    />
  </div>
</template>
```

### Position

```vue
<template>
  <div class="image-demo">
    <van-image
      width="10rem"
      height="10rem"
      fit="cover"
      position="left"
      src="https://fastly.jsdelivr.net/npm/@vant/assets/cat.jpeg"
    />
    <van-image
      width="10rem"
      height="10rem"
      fit="cover"
      position="right"
      src="https://fastly.jsdelivr.net/npm/@vant/assets/cat.jpeg"
    />
  </div>
</template>
```

### Round Image

```vue
<template>
  <van-image
    round
    width="10rem"
    height="10rem"
    src="https://fastly.jsdelivr.net/npm/@vant/assets/cat.jpeg"
  />
</template>
```

### Border Radius

```vue
<template>
  <van-image
    width="100"
    height="100"
    radius="10px"
    src="https://fastly.jsdelivr.net/npm/@vant/assets/cat.jpeg"
  />
</template>
```

### Lazy Load

```vue
<template>
  <van-image
    width="100"
    height="100"
    lazy-load
    src="https://fastly.jsdelivr.net/npm/@vant/assets/cat.jpeg"
  />
</template>

<script setup>
import { createApp } from 'vue'
import { Lazyload } from 'vant'

const app = createApp()
app.use(Lazyload)
</script>
```

### Custom Loading Placeholder

```vue
<template>
  <van-image
    width="100"
    height="100"
    src="https://fastly.jsdelivr.net/npm/@vant/assets/cat.jpeg"
  >
    <template #loading>
      <van-loading type="spinner" size="20" />
    </template>
  </van-image>
</template>
```

### Custom Error Placeholder

```vue
<template>
  <van-image
    width="100"
    height="100"
    src="invalid-url.jpg"
  >
    <template #error>
      <div class="error-placeholder">Load failed</div>
    </template>
  </van-image>
</template>

<style scoped>
.error-placeholder {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
  background: #f7f8fa;
  color: #969799;
}
</style>
```

### Image Gallery

```vue
<template>
  <div class="gallery">
    <van-image
      v-for="(image, index) in images"
      :key="index"
      width="100%"
      height="200"
      fit="cover"
      :src="image"
      @click="previewImage(index)"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { showImagePreview } from 'vant'

const images = ref([
  'https://fastly.jsdelivr.net/npm/@vant/assets/cat.jpeg',
  'https://fastly.jsdelivr.net/npm/@vant/assets/apple-1.jpeg',
  'https://fastly.jsdelivr.net/npm/@vant/assets/apple-2.jpeg',
])

const previewImage = (index) => {
  showImagePreview({
    images: images.value,
    startPosition: index,
  })
}
</script>

<style scoped>
.gallery {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 8px;
}
</style>
```

### Avatar Image

```vue
<template>
  <van-image
    round
    width="60"
    height="60"
    fit="cover"
    src="https://fastly.jsdelivr.net/npm/@vant/assets/cat.jpeg"
  />
</template>
```

### Responsive Image

```vue
<template>
  <van-image
    width="100%"
    height="auto"
    fit="contain"
    src="https://fastly.jsdelivr.net/npm/@vant/assets/cat.jpeg"
  />
</template>
```

### Image with Events

```vue
<template>
  <van-image
    width="100"
    height="100"
    :src="imageSrc"
    @load="onLoad"
    @error="onError"
    @click="onClick"
  />
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const imageSrc = ref('https://fastly.jsdelivr.net/npm/@vant/assets/cat.jpeg')

const onLoad = () => {
  showToast('Image loaded')
}

const onError = () => {
  showToast('Image load failed')
}

const onClick = () => {
  showToast('Image clicked')
}
</script>
```

### Image List with Lazy Load

```vue
<template>
  <div class="image-list">
    <van-image
      v-for="(image, index) in images"
      :key="index"
      width="100%"
      height="200"
      fit="cover"
      lazy-load
      :src="image"
    />
  </div>
</template>

<script setup>
const images = Array.from({ length: 20 }, (_, i) => 
  `https://picsum.photos/400/300?random=${i}`
)
</script>

<style scoped>
.image-list {
  display: flex;
  flex-direction: column;
  gap: 8px;
}
</style>
```

### Block Image

```vue
<template>
  <van-image
    block
    width="100%"
    height="200"
    fit="cover"
    src="https://fastly.jsdelivr.net/npm/@vant/assets/cat.jpeg"
  />
</template>
```

### Image with Overlay

```vue
<template>
  <van-image
    width="100%"
    height="200"
    fit="cover"
    src="https://fastly.jsdelivr.net/npm/@vant/assets/cat.jpeg"
  >
    <div class="overlay">
      <span class="overlay-text">Image Caption</span>
    </div>
  </van-image>
</template>

<style scoped>
.overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 8px;
  background: linear-gradient(transparent, rgba(0, 0, 0, 0.5));
}

.overlay-text {
  color: white;
  font-size: 14px;
}
</style>
```

### Image with Badge

```vue
<template>
  <van-badge :content="badge">
    <van-image
      width="100"
      height="100"
      fit="cover"
      src="https://fastly.jsdelivr.net/npm/@vant/assets/cat.jpeg"
    />
  </van-badge>
</template>

<script setup>
import { ref } from 'vue'

const badge = ref('New')
</script>
```

## Common Issues

### 1. Round Image Not Working with Contain

Round may not work correctly with `fit="contain"` or `fit="scale-down"`:

```vue
<!-- Use cover for round images -->
<van-image round fit="cover" src="..." />
```

### 2. Lazy Load Not Working

Make sure to register the Lazyload plugin:

```js
import { Lazyload } from 'vant'

app.use(Lazyload)
```

### 3. Image Not Displaying

Check if the image URL is correct and accessible:

```vue
<van-image
  :src="imageUrl"
  @error="handleError"
/>
```

### 4. Aspect Ratio Issues

Use `fit="contain"` to maintain aspect ratio:

```vue
<van-image width="200" height="200" fit="contain" src="..." />
```

## Component Interactions

### With ImagePreview

```vue
<template>
  <van-image
    width="100"
    height="100"
    :src="image"
    @click="showPreview"
  />
</template>

<script setup>
import { showImagePreview } from 'vant'

const image = 'https://fastly.jsdelivr.net/npm/@vant/assets/cat.jpeg'

const showPreview = () => {
  showImagePreview([image])
}
</script>
```

### With Swipe

```vue
<template>
  <van-swipe :autoplay="3000">
    <van-swipe-item v-for="(image, index) in images" :key="index">
      <van-image width="100%" height="200" fit="cover" :src="image" />
    </van-swipe-item>
  </van-swipe>
</template>

<script setup>
const images = [
  'https://fastly.jsdelivr.net/npm/@vant/assets/cat.jpeg',
  'https://fastly.jsdelivr.net/npm/@vant/assets/apple-1.jpeg',
  'https://fastly.jsdelivr.net/npm/@vant/assets/apple-2.jpeg',
]
</script>
```

### With Lazyload Options

```vue
<template>
  <van-image
    width="100"
    height="100"
    lazy-load
    src="https://fastly.jsdelivr.net/npm/@vant/assets/cat.jpeg"
  />
</template>

<script setup>
import { Lazyload } from 'vant'

app.use(Lazyload, {
  lazyComponent: true,
  loading: 'loading.png',
  error: 'error.png',
})
</script>
```

## Best Practices

1. **Use appropriate fit mode**: Choose the right fit mode for your use case
2. **Lazy load for performance**: Use lazy loading for images below the fold
3. **Provide placeholders**: Always provide loading and error placeholders
4. **Optimize images**: Use optimized images for better performance
5. **Alt text**: Add meaningful alt text for accessibility
6. **Responsive images**: Use percentage widths for responsive layouts
7. **Error handling**: Handle image load errors gracefully
8. **Aspect ratio**: Maintain aspect ratio with appropriate fit modes
9. **Touch targets**: Make clickable images large enough for touch
10. **Image optimization**: Use appropriate image formats and sizes
