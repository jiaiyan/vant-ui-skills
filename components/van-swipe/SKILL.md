---
name: "van-swipe"
description: "Swipe carousel component for looping images or content. Invoke when user needs to create image carousels, content sliders, or swipeable galleries."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Swipe Component

Used to loop a group of pictures or content with touch swipe support.

## When to Invoke

Invoke this skill when:
- User needs to create image carousels or sliders
- User wants to implement swipeable content galleries
- User needs to create banner rotation effects
- User asks about touch swipe components
- User wants to create vertical or horizontal swipers

## Features

- **Auto Play**: Configurable auto-play interval
- **Loop Mode**: Infinite loop scrolling
- **Touch Support**: Swipe gestures for navigation
- **Vertical/Horizontal**: Support for both directions
- **Lazy Rendering**: Performance optimization with lazy render
- **Custom Indicators**: Customizable indicator display
- **Programmatic Control**: Methods for navigation control
- **Custom Item Size**: Configurable swipe item dimensions

## API Reference

### Swipe Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| autoplay | Autoplay interval (ms) | `number \| string` | - |
| duration | Animation duration (ms) | `number \| string` | `500` |
| initial-swipe | Index of initial swipe, start from 0 | `number \| string` | `0` |
| width | Width of swipe item | `number \| string` | `0` |
| height | Height of swipe item | `number \| string` | `0` |
| loop | Whether to enable loop | `boolean` | `true` |
| show-indicators | Whether to show indicators | `boolean` | `true` |
| vertical | Whether to be vertical scrolling | `boolean` | `false` |
| touchable | Whether to allow swipe by touch gesture | `boolean` | `true` |
| stop-propagation | Whether to stop touchmove event propagation | `boolean` | `false` |
| lazy-render | Whether to enable lazy render | `boolean` | `false` |
| indicator-color | Indicator color | `string` | `#1989fa` |

### Swipe Events

| Name | Description | Arguments |
|------|-------------|-----------|
| change | Emitted when current swipe changed | `index: number` |
| drag-start | Emitted when user starts dragging the swipe | `{ index: number }` |
| drag-end | Emitted when user ends dragging the swipe | `{ index: number }` |

### SwipeItem Events

| Name | Description | Arguments |
|------|-------------|-----------|
| click | Emitted when component is clicked | `event: MouseEvent` |

### Swipe Methods

Use ref to get Swipe instance and call instance methods.

| Name | Description | Arguments | Return Value |
|------|-------------|-----------|--------------|
| prev | Swipe to prev item | - | - |
| next | Swipe to next item | - | - |
| swipeTo | Swipe to target index | `index: number, options: SwipeToOptions` | - |
| resize | Resize Swipe when container element resized or visibility changed | - | - |

### SwipeToOptions

| Name | Description | Type |
|------|-------------|------|
| immediate | Whether to skip animation | `boolean` |

### Swipe Slots

| Name | Description | SlotProps |
|------|-------------|-----------|
| default | Content | - |
| indicator | Custom indicator | `{ active: number, total: number }` |

### Types

```ts
import type { SwipeProps, SwipeInstance, SwipeToOptions } from 'vant';
```

### CSS Variables

| Name | Default Value | Description |
|------|---------------|-------------|
| --van-swipe-indicator-size | `6px` | Indicator size |
| --van-swipe-indicator-margin | `var(--van-padding-sm)` | Indicator margin |
| --van-swipe-indicator-active-opacity | `1` | Active indicator opacity |
| --van-swipe-indicator-inactive-opacity | `0.3` | Inactive indicator opacity |
| --van-swipe-indicator-active-background | `var(--van-primary-color)` | Active indicator background |
| --van-swipe-indicator-inactive-background | `var(--van-border-color)` | Inactive indicator background |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-swipe class="my-swipe" :autoplay="3000" indicator-color="white">
    <van-swipe-item>1</van-swipe-item>
    <van-swipe-item>2</van-swipe-item>
    <van-swipe-item>3</van-swipe-item>
    <van-swipe-item>4</van-swipe-item>
  </van-swipe>
</template>

<style>
.my-swipe .van-swipe-item {
  color: #fff;
  font-size: 20px;
  line-height: 150px;
  text-align: center;
  background-color: #39a9ed;
}
</style>
```

### Image Carousel

```vue
<template>
  <van-swipe :autoplay="3000" lazy-render>
    <van-swipe-item v-for="image in images" :key="image">
      <img :src="image" style="width: 100%; height: 240px; object-fit: cover;" />
    </van-swipe-item>
  </van-swipe>
</template>

<script setup>
import { ref } from 'vue';

const images = ref([
  'https://fastly.jsdelivr.net/npm/@vant/assets/apple-1.jpeg',
  'https://fastly.jsdelivr.net/npm/@vant/assets/apple-2.jpeg',
  'https://fastly.jsdelivr.net/npm/@vant/assets/apple-3.jpeg',
  'https://fastly.jsdelivr.net/npm/@vant/assets/apple-4.jpeg',
]);
</script>
```

### Change Event

```vue
<template>
  <van-swipe @change="onChange">
    <van-swipe-item>1</van-swipe-item>
    <van-swipe-item>2</van-swipe-item>
    <van-swipe-item>3</van-swipe-item>
    <van-swipe-item>4</van-swipe-item>
  </van-swipe>
</template>

<script setup>
import { showToast } from 'vant';

const onChange = (index) => {
  showToast(`Current Swipe index: ${index}`);
};
</script>
```

### Vertical Scrolling

```vue
<template>
  <van-swipe :autoplay="3000" vertical style="height: 200px;">
    <van-swipe-item>1</van-swipe-item>
    <van-swipe-item>2</van-swipe-item>
    <van-swipe-item>3</van-swipe-item>
    <van-swipe-item>4</van-swipe-item>
  </van-swipe>
</template>
```

### Set SwipeItem Size

```vue
<template>
  <van-swipe :loop="false" :width="300">
    <van-swipe-item>1</van-swipe-item>
    <van-swipe-item>2</van-swipe-item>
    <van-swipe-item>3</van-swipe-item>
    <van-swipe-item>4</van-swipe-item>
  </van-swipe>
</template>
```

### Custom Indicator

```vue
<template>
  <van-swipe @change="onChange">
    <van-swipe-item>1</van-swipe-item>
    <van-swipe-item>2</van-swipe-item>
    <van-swipe-item>3</van-swipe-item>
    <van-swipe-item>4</van-swipe-item>
    <template #indicator="{ active, total }">
      <div class="custom-indicator">{{ active + 1 }}/{{ total }}</div>
    </template>
  </van-swipe>
</template>

<style>
.custom-indicator {
  position: absolute;
  right: 5px;
  bottom: 5px;
  padding: 2px 5px;
  font-size: 12px;
  background: rgba(0, 0, 0, 0.1);
  color: #fff;
}
</style>
```

### Manual Control

```vue
<template>
  <van-swipe ref="swipeRef" :loop="false">
    <van-swipe-item>1</van-swipe-item>
    <van-swipe-item>2</van-swipe-item>
    <van-swipe-item>3</van-swipe-item>
  </van-swipe>
  
  <div class="controls">
    <van-button @click="prev">Previous</van-button>
    <van-button @click="next">Next</van-button>
    <van-button @click="goTo(1)">Go to 2</van-button>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const swipeRef = ref(null);

const prev = () => {
  swipeRef.value?.prev();
};

const next = () => {
  swipeRef.value?.next();
};

const goTo = (index) => {
  swipeRef.value?.swipeTo(index);
};
</script>
```

### Product Gallery

```vue
<template>
  <div class="product-gallery">
    <van-swipe ref="galleryRef" @change="onGalleryChange">
      <van-swipe-item v-for="(image, index) in productImages" :key="index">
        <img :src="image" class="product-image" />
      </van-swipe-item>
      <template #indicator="{ active, total }">
        <div class="gallery-indicator">{{ active + 1 }}/{{ total }}</div>
      </template>
    </van-swipe>
    
    <div class="thumbnails">
      <img
        v-for="(image, index) in productImages"
        :key="index"
        :src="image"
        :class="{ active: currentIndex === index }"
        @click="selectImage(index)"
        class="thumbnail"
      />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const galleryRef = ref(null);
const currentIndex = ref(0);

const productImages = ref([
  'https://fastly.jsdelivr.net/npm/@vant/assets/apple-1.jpeg',
  'https://fastly.jsdelivr.net/npm/@vant/assets/apple-2.jpeg',
  'https://fastly.jsdelivr.net/npm/@vant/assets/apple-3.jpeg',
  'https://fastly.jsdelivr.net/npm/@vant/assets/apple-4.jpeg',
]);

const onGalleryChange = (index) => {
  currentIndex.value = index;
};

const selectImage = (index) => {
  galleryRef.value?.swipeTo(index);
};
</script>

<style>
.product-gallery {
  background: #fff;
}

.product-image {
  width: 100%;
  height: 300px;
  object-fit: cover;
}

.gallery-indicator {
  position: absolute;
  right: 10px;
  bottom: 10px;
  padding: 4px 8px;
  background: rgba(0, 0, 0, 0.5);
  color: #fff;
  border-radius: 4px;
  font-size: 12px;
}

.thumbnails {
  display: flex;
  gap: 8px;
  padding: 12px;
  overflow-x: auto;
}

.thumbnail {
  width: 60px;
  height: 60px;
  object-fit: cover;
  border-radius: 4px;
  border: 2px solid transparent;
  cursor: pointer;
}

.thumbnail.active {
  border-color: #1989fa;
}
</style>
```

### Banner Carousel

```vue
<template>
  <van-swipe :autoplay="4000" class="banner-swipe">
    <van-swipe-item v-for="banner in banners" :key="banner.id">
      <div class="banner-item" :style="{ background: banner.color }">
        <h3>{{ banner.title }}</h3>
        <p>{{ banner.subtitle }}</p>
      </div>
    </van-swipe-item>
  </van-swipe>
</template>

<script setup>
import { ref } from 'vue';

const banners = ref([
  { id: 1, title: 'New Arrivals', subtitle: 'Check out our latest products', color: '#1989fa' },
  { id: 2, title: 'Summer Sale', subtitle: 'Up to 50% off', color: '#07c160' },
  { id: 3, title: 'Free Shipping', subtitle: 'On orders over $50', color: '#ff976a' },
]);
</script>

<style>
.banner-swipe {
  height: 160px;
}

.banner-item {
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  color: #fff;
}

.banner-item h3 {
  margin: 0 0 8px;
  font-size: 24px;
}

.banner-item p {
  margin: 0;
  font-size: 14px;
  opacity: 0.9;
}
</style>
```

## Best Practices

1. **Use lazy-render for performance**: Enable `lazy-render` when displaying many images
2. **Set appropriate autoplay**: Balance between user experience and content visibility
3. **Custom indicators for better UX**: Use custom indicators for more context
4. **Handle resize events**: Call `resize()` method when container size changes
5. **Disable loop for fixed width**: Set `loop="false"` when using custom item width
