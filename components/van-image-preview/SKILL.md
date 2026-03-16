---
name: "van-image-preview"
description: "Image preview component for displaying and zooming images. Invoke when user needs to implement image galleries, photo viewers, or image zoom functionality."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant ImagePreview Component

Used to zoom in and preview images, supporting both function call and component usage.

## When to Invoke

Invoke this skill when:
- User needs to implement image preview functionality
- User wants to create image galleries or photo viewers
- User needs zoom and swipe gestures for images
- User wants to preview images with custom content
- User asks about programmatic image preview control

## Features

- **Function Call**: Quick invocation via `showImagePreview` function
- **Component Usage**: Full component control with slots
- **Zoom Support**: Pinch-to-zoom and double-tap zoom
- **Swipe Navigation**: Swipe between multiple images
- **Custom Content**: Support custom index and image slots
- **Close Control**: Configurable close behavior
- **Event Callbacks**: Multiple events for interaction handling

## API Reference

### Methods

| Name | Description | Attribute | Return value |
|------|-------------|-----------|--------------|
| showImagePreview | Display a full-screen image preview component | `string[] \| ImagePreviewOptions` | ImagePreview Instance |

### ImagePreviewOptions

| Name | Description | Type | Default |
|------|-------------|------|---------|
| images | Images URL list | `string[]` | `[]` |
| startPosition | Start position | `number \| string` | `0` |
| showIndex | Whether to show index | `boolean` | `true` |
| showIndicators | Whether to show indicators | `boolean` | `false` |
| loop | Whether to enable loop | `boolean` | `true` |
| swipeDuration | Animation duration (ms) | `number \| string` | `300` |
| onClose | Emitted when ImagePreview is closed | `Function` | - |
| onChange | Emitted when current image changed | `Function` | - |
| onScale | Emitted when scaling current image | `Function` | - |
| closeOnPopstate | Whether to close when popstate | `boolean` | `true` |
| doubleScale | Whether to enable double tap zoom gesture | `boolean` | `true` |
| closeOnClickImage | Whether to close when image is clicked | `boolean` | `true` |
| closeOnClickOverlay | Whether to close when overlay is clicked | `boolean` | `true` |
| vertical | Whether to enable vertical gesture sliding | `boolean` | `false` |
| beforeClose | Callback function before close | `(action) => boolean \| Promise` | - |
| className | Custom className | `string \| Array \| object` | - |
| maxZoom | Max zoom | `number \| string` | `3` |
| minZoom | Min zoom | `number \| string` | `1/3` |
| closeable | Whether to show close icon | `boolean` | `false` |
| closeIcon | Close icon name | `string` | `clear` |
| closeIconPosition | Close icon position | `string` | `top-right` |
| transition | Transition | `string` | `van-fade` |
| overlayClass | Custom overlay class | `string \| Array \| object` | - |
| overlayStyle | Custom overlay style | `object` | - |
| teleport | Specifies a target element | `string \| Element` | - |

### Props (Component Usage)

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model:show | Whether to show ImagePreview | `boolean` | `false` |
| images | Images URL list | `string[]` | `[]` |
| start-position | Start position | `number \| string` | `0` |
| swipe-duration | Animation duration (ms) | `number \| string` | `300` |
| show-index | Whether to show index | `boolean` | `true` |
| show-indicators | Whether to show indicators | `boolean` | `false` |
| loop | Whether to enable loop | `boolean` | `true` |
| double-scale | Whether to enable double tap zoom | `boolean` | `true` |
| before-close | Callback function before close | `(action: number) => boolean \| Promise<boolean>` | - |
| close-on-popstate | Whether to close when popstate | `boolean` | `true` |
| close-on-click-image | Whether to close when image is clicked | `boolean` | `true` |
| close-on-click-overlay | Whether to close when overlay is clicked | `boolean` | `true` |
| vertical | Whether to enable vertical gesture | `boolean` | `false` |
| class-name | Custom className | `string \| Array \| object` | - |
| max-zoom | Max zoom | `number \| string` | `3` |
| min-zoom | Min zoom | `number \| string` | `1/3` |
| closeable | Whether to show close icon | `boolean` | `false` |
| close-icon | Close icon name | `string` | `clear` |
| close-icon-position | Close icon position | `string` | `top-right` |
| transition | Transition | `string` | `van-fade` |
| overlay-class | Custom overlay class | `string \| Array \| object` | - |
| overlay-style | Custom overlay style | `object` | - |
| teleport | Specifies a target element | `string \| Element` | - |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| close | Emitted when closing ImagePreview | `{ index: number, url: string }` |
| closed | Emitted when ImagePreview is closed | - |
| change | Emitted when current image changed | `index: number` |
| scale | Emitted when scaling current image | `{ index: number, scale: number }` |
| long-press | Emitted when long press current image | `{ index: number }` |

### Methods (Component)

| Name | Description | Attribute | Return value |
|------|-------------|-----------|--------------|
| resetScale | Reset the current image's zoom ratio | - | - |
| swipeTo | Swipe to target index | `index: number, options?: SwipeToOptions` | - |

### Slots

| Name | Description | SlotProps |
|------|-------------|-----------|
| index | Custom index | `{ index: index of current image }` |
| cover | Custom content that covers the preview | - |
| image | Custom image content | `{ src, onLoad, style }` |

### Types

```ts
import type {
  ImagePreviewProps,
  ImagePreviewOptions,
  ImagePreviewInstance,
  ImagePreviewScaleEventParams,
} from 'vant';
```

## Usage Examples

### Basic Usage (Function Call)

```vue
<template>
  <van-button @click="showPreview">Show Preview</van-button>
</template>

<script setup>
import { showImagePreview } from 'vant';

const showPreview = () => {
  showImagePreview([
    'https://fastly.jsdelivr.net/npm/@vant/assets/apple-1.jpeg',
    'https://fastly.jsdelivr.net/npm/@vant/assets/apple-2.jpeg',
  ]);
};
</script>
```

### Set Start Position

```vue
<template>
  <van-button @click="showPreview">Show Preview</van-button>
</template>

<script setup>
import { showImagePreview } from 'vant';

const showPreview = () => {
  showImagePreview({
    images: [
      'https://fastly.jsdelivr.net/npm/@vant/assets/apple-1.jpeg',
      'https://fastly.jsdelivr.net/npm/@vant/assets/apple-2.jpeg',
    ],
    startPosition: 1,
  });
};
</script>
```

### Show Close Icon

```vue
<template>
  <van-button @click="showPreview">Show Preview</van-button>
</template>

<script setup>
import { showImagePreview } from 'vant';

const showPreview = () => {
  showImagePreview({
    images: [
      'https://fastly.jsdelivr.net/npm/@vant/assets/apple-1.jpeg',
      'https://fastly.jsdelivr.net/npm/@vant/assets/apple-2.jpeg',
    ],
    closeable: true,
  });
};
</script>
```

### Close Event

```vue
<template>
  <van-button @click="showPreview">Show Preview</van-button>
</template>

<script setup>
import { showToast, showImagePreview } from 'vant';

const showPreview = () => {
  showImagePreview({
    images: [
      'https://fastly.jsdelivr.net/npm/@vant/assets/apple-1.jpeg',
      'https://fastly.jsdelivr.net/npm/@vant/assets/apple-2.jpeg',
    ],
    onClose() {
      showToast('closed');
    },
  });
};
</script>
```

### Before Close

```vue
<template>
  <van-button @click="showPreview">Show Preview</van-button>
</template>

<script setup>
import { showImagePreview } from 'vant';

const showPreview = () => {
  const instance = showImagePreview({
    images: [
      'https://fastly.jsdelivr.net/npm/@vant/assets/apple-1.jpeg',
      'https://fastly.jsdelivr.net/npm/@vant/assets/apple-2.jpeg',
    ],
    beforeClose: () => false,
  });

  setTimeout(() => {
    instance.close();
  }, 2000);
};
</script>
```

### Component Usage

```vue
<template>
  <van-button @click="show = true">Show Preview</van-button>
  <van-image-preview v-model:show="show" :images="images" @change="onChange">
    <template #index>Page: {{ index + 1 }}</template>
  </van-image-preview>
</template>

<script setup>
import { ref } from 'vue';

const show = ref(false);
const index = ref(0);
const images = [
  'https://fastly.jsdelivr.net/npm/@vant/assets/apple-1.jpeg',
  'https://fastly.jsdelivr.net/npm/@vant/assets/apple-2.jpeg',
];

const onChange = (newIndex) => {
  index.value = newIndex;
};
</script>
```

### Custom Image Slot (Video)

```vue
<template>
  <van-image-preview
    v-model:show="show"
    :images="images"
    :close-on-click-image="false"
  >
    <template #image="{ src }">
      <video style="width: 100%;" controls>
        <source :src="src" />
      </video>
    </template>
  </van-image-preview>
</template>

<script setup>
import { ref } from 'vue';

const show = ref(false);
const images = [
  'https://www.w3school.com.cn/i/movie.ogg',
  'https://www.w3school.com.cn/i/movie.ogg',
];
</script>
```

## Common Issues

### 1. Images Not Loading

Ensure image URLs are accessible and properly formatted:

```js
showImagePreview({
  images: ['https://example.com/image.jpg'],
});
```

### 2. Programmatic Close

Use the instance returned by `showImagePreview`:

```js
const instance = showImagePreview({ images: [...] });
instance.close();
```

### 3. Custom Index Display

Use the `index` slot for custom formatting:

```vue
<van-image-preview v-model:show="show" :images="images">
  <template #index="{ index }">
    {{ index + 1 }} / {{ images.length }}
  </template>
</van-image-preview>
```

## Component Interactions

### With Image Grid

```vue
<template>
  <van-grid :column-num="3">
    <van-grid-item 
      v-for="(image, index) in images" 
      :key="index"
      @click="showPreview(index)"
    >
      <van-image :src="image" />
    </van-grid-item>
  </van-grid>
</template>

<script setup>
import { ref } from 'vue';
import { showImagePreview } from 'vant';

const images = ref([
  'https://fastly.jsdelivr.net/npm/@vant/assets/apple-1.jpeg',
  'https://fastly.jsdelivr.net/npm/@vant/assets/apple-2.jpeg',
  'https://fastly.jsdelivr.net/npm/@vant/assets/apple-3.jpeg',
]);

const showPreview = (startPosition) => {
  showImagePreview({
    images: images.value,
    startPosition,
  });
};
</script>
```

### With Long Press

```vue
<template>
  <van-button @click="showPreview">Show Preview</van-button>
</template>

<script setup>
import { showImagePreview, showToast } from 'vant';

const showPreview = () => {
  showImagePreview({
    images: ['https://fastly.jsdelivr.net/npm/@vant/assets/apple-1.jpeg'],
    onLongPress: ({ index }) => {
      showToast('Long pressed');
    },
  });
};
</script>
```

## Best Practices

1. **Optimize images**: Use appropriately sized images for better performance
2. **Provide close option**: Always provide a way to close the preview
3. **Handle errors**: Handle image loading errors gracefully
4. **Accessibility**: Ensure preview is accessible with keyboard navigation
5. **Mobile gestures**: Test zoom and swipe gestures on mobile devices
