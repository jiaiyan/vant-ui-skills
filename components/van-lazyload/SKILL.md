---
name: "van-lazyload"
description: "Lazyload directive for delaying content loading outside the visible area. Invoke when user needs to implement lazy loading for images or components."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Lazyload Directive

When the page needs to load a large amount of content, delay loading the content outside the visible area to make the page load smoother.

## When to Invoke

Invoke this skill when:
- User needs to implement lazy loading for images
- User wants to improve page performance with lazy loading
- User needs to lazy load components
- User wants to set loading and error placeholders
- User asks about background image lazy loading

## Features

- **Image Lazy Loading**: Delay loading images outside viewport
- **Background Image**: Support lazy loading for background images
- **Component Lazy Loading**: Lazy load entire components
- **Loading Placeholder**: Custom loading state images
- **Error Placeholder**: Custom error state images
- **Pre-load Control**: Configurable pre-load distance
- **Event Listeners**: Custom scroll event listeners

## API Reference

### Options

| Name | Description | Type | Default |
|------|-------------|------|---------|
| loading | Src of the image while loading | `string` | - |
| error | Src of the image upon load fail | `string` | - |
| preLoad | Proportion of pre-loading height | `number` | - |
| attempt | Attempts count | `number` | `3` |
| listenEvents | Events that you want vue listen for | `string[]` | `scroll`... |
| adapter | Dynamically modify the attribute of element | `object` | - |
| filter | The image's listener filter | `object` | - |
| lazyComponent | Lazyload component | `boolean` | `false` |

## Usage Examples

### Basic Usage

```vue
<template>
  <img v-for="img in imageList" v-lazy="img" />
</template>

<script setup>
import { ref } from 'vue';

const imageList = ref([
  'https://fastly.jsdelivr.net/npm/@vant/assets/apple-1.jpeg',
  'https://fastly.jsdelivr.net/npm/@vant/assets/apple-2.jpeg',
]);
</script>
```

### Lazyload Background Image

```vue
<template>
  <div 
    v-for="img in imageList" 
    v-lazy:background-image="img"
    class="bg-image"
  />
</template>

<script setup>
import { ref } from 'vue';

const imageList = ref([
  'https://fastly.jsdelivr.net/npm/@vant/assets/apple-1.jpeg',
  'https://fastly.jsdelivr.net/npm/@vant/assets/apple-2.jpeg',
]);
</script>

<style scoped>
.bg-image {
  width: 100%;
  height: 200px;
  background-size: cover;
  background-position: center;
}
</style>
```

### With Loading and Error Images

```js
import { createApp } from 'vue';
import { Lazyload } from 'vant';

const app = createApp();

app.use(Lazyload, {
  loading: 'https://example.com/loading.png',
  error: 'https://example.com/error.png',
});
```

### Lazyload Component

```js
import { createApp } from 'vue';
import { Lazyload } from 'vant';

const app = createApp();

app.use(Lazyload, {
  lazyComponent: true,
});
```

```vue
<template>
  <lazy-component>
    <img v-for="img in imageList" v-lazy="img" />
  </lazy-component>
</template>
```

### With VanImage Component

```vue
<template>
  <van-image
    v-for="img in imageList"
    :key="img"
    v-lazy="img"
    width="100%"
    height="200"
    fit="cover"
  />
</template>

<script setup>
import { ref } from 'vue';

const imageList = ref([
  'https://fastly.jsdelivr.net/npm/@vant/assets/apple-1.jpeg',
  'https://fastly.jsdelivr.net/npm/@vant/assets/apple-2.jpeg',
]);
</script>
```

### Custom Configuration

```js
import { createApp } from 'vue';
import { Lazyload } from 'vant';

const app = createApp();

app.use(Lazyload, {
  preLoad: 1.3,
  error: 'error.png',
  loading: 'loading.png',
  attempt: 1,
  lazyComponent: true,
});
```

## Common Issues

### 1. Images Not Loading

Ensure Lazyload is properly registered:

```js
import { createApp } from 'vue';
import { Lazyload } from 'vant';

const app = createApp();
app.use(Lazyload);
```

### 2. Background Image Not Working

Use `v-lazy:background-image` syntax:

```vue
<div v-lazy:background-image="imageUrl"></div>
```

### 3. Component Not Lazy Loading

Enable `lazyComponent` option:

```js
app.use(Lazyload, {
  lazyComponent: true,
});
```

### 4. Scroll Container Issues

For custom scroll containers, ensure proper event listeners:

```js
app.use(Lazyload, {
  listenEvents: ['scroll'],
});
```

## Component Interactions

### With List Component

```vue
<template>
  <van-list
    v-model:loading="loading"
    :finished="finished"
    @load="onLoad"
  >
    <van-cell v-for="item in list" :key="item.id">
      <img v-lazy="item.image" />
    </van-cell>
  </van-list>
</template>

<script setup>
import { ref } from 'vue';

const list = ref([]);
const loading = ref(false);
const finished = ref(false);

const onLoad = () => {
  setTimeout(() => {
    for (let i = 0; i < 10; i++) {
      list.value.push({
        id: list.value.length + 1,
        image: `https://picsum.photos/200/200?random=${list.value.length}`,
      });
    }
    loading.value = false;
    if (list.value.length >= 40) {
      finished.value = true;
    }
  }, 1000);
};
</script>
```

### With Image Gallery

```vue
<template>
  <van-grid :column-num="2">
    <van-grid-item v-for="img in images" :key="img">
      <van-image v-lazy="img" fit="cover" />
    </van-grid-item>
  </van-grid>
</template>

<script setup>
import { ref } from 'vue';

const images = ref([
  'https://fastly.jsdelivr.net/npm/@vant/assets/apple-1.jpeg',
  'https://fastly.jsdelivr.net/npm/@vant/assets/apple-2.jpeg',
  'https://fastly.jsdelivr.net/npm/@vant/assets/apple-3.jpeg',
]);
</script>
```

### With Card List

```vue
<template>
  <van-card v-for="product in products" :key="product.id">
    <template #thumb>
      <img v-lazy="product.image" />
    </template>
    <template #title>
      {{ product.title }}
    </template>
    <template #desc>
      {{ product.description }}
    </template>
  </van-card>
</template>

<script setup>
import { ref } from 'vue';

const products = ref([
  {
    id: 1,
    title: 'Product 1',
    description: 'Description 1',
    image: 'https://fastly.jsdelivr.net/npm/@vant/assets/apple-1.jpeg',
  },
]);
</script>
```

## Best Practices

1. **Use loading placeholders**: Provide loading images for better user experience
2. **Handle errors**: Set error images for failed loads
3. **Optimize pre-load**: Adjust preLoad based on your layout
4. **Test on slow networks**: Verify lazy loading behavior on slow connections
5. **Consider SEO**: For SEO-critical images, avoid lazy loading
