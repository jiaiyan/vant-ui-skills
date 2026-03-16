---
name: "van-skeleton"
description: "Skeleton loading placeholder component. Invoke when user needs to display loading placeholders, content loading states, or improve perceived loading performance."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Skeleton Component

Used to display a set of placeholder graphics during the content loading process, improving perceived performance.

## When to Invoke

Invoke this skill when:
- User needs to display loading placeholders
- User wants to improve perceived loading performance
- User needs skeleton screens for content loading
- User asks about loading state UI patterns
- User wants to create custom skeleton layouts

## Features

- **Row Placeholder**: Display multiple row placeholders
- **Avatar Placeholder**: Optional avatar placeholder
- **Title Placeholder**: Optional title placeholder
- **Custom Content**: Template slot for custom layouts
- **Animation**: Configurable animation effect
- **Round Style**: Option for rounded placeholders
- **Loading Toggle**: Switch between skeleton and actual content

## API Reference

### Skeleton Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| row | Row count | `number \| string` | `0` |
| row-width | Row width, can be array | `number \| string \| (number \| string)[]` | `100%` |
| title | Whether to show title placeholder | `boolean` | `false` |
| avatar | Whether to show avatar placeholder | `boolean` | `false` |
| loading | Whether to show skeleton, pass `false` to show child component | `boolean` | `true` |
| animate | Whether to enable animation | `boolean` | `true` |
| round | Whether to show round title and paragraph | `boolean` | `false` |
| title-width | Title width | `number \| string` | `40%` |
| avatar-size | Size of avatar placeholder | `number \| string` | `32px` |
| avatar-shape | Shape of avatar placeholder, can be set to `square` | `string` | `round` |

### Skeleton Slots

| Name | Description |
|------|-------------|
| default | Default slot for actual content |
| template | Custom skeleton content |

### Types

```ts
import type {
  SkeletonProps,
  SkeletonImageProps,
  SkeletonTitleProps,
  SkeletonAvatarShape,
  SkeletonImageShape,
  SkeletonParagraphProps,
} from 'vant';
```

### CSS Variables

| Name | Default Value | Description |
|------|---------------|-------------|
| --van-skeleton-row-height | `16px` | Height of skeleton rows |
| --van-skeleton-row-background | `var(--van-active-color)` | Background color of rows |
| --van-skeleton-row-margin-top | `var(--van-padding-sm)` | Margin top of rows |
| --van-skeleton-title-width | `40%` | Width of title |
| --van-skeleton-avatar-size | `32px` | Size of avatar |
| --van-skeleton-avatar-background | `var(--van-active-color)` | Avatar background color |
| --van-skeleton-duration | `1.2s` | Animation duration |
| --van-skeleton-image-size | `96px` | Image placeholder size |
| --van-skeleton-image-radius | `24px` | Image placeholder radius |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-skeleton title :row="3" />
</template>
```

### Show Avatar

```vue
<template>
  <van-skeleton title avatar :row="3" />
</template>
```

### Show Children After Loading

```vue
<template>
  <van-skeleton title avatar :row="3" :loading="loading">
    <div class="content">
      <h3>Actual Content</h3>
      <p>This is the real content that appears after loading.</p>
    </div>
  </van-skeleton>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const loading = ref(true);

onMounted(() => {
  setTimeout(() => {
    loading.value = false;
  }, 2000);
});
</script>
```

### Custom Content

```vue
<template>
  <van-skeleton>
    <template #template>
      <div :style="{ display: 'flex', width: '100%' }">
        <van-skeleton-image />
        <div :style="{ flex: 1, marginLeft: '16px' }">
          <van-skeleton-paragraph row-width="60%" />
          <van-skeleton-paragraph />
          <van-skeleton-paragraph />
          <van-skeleton-paragraph />
        </div>
      </div>
    </template>
  </van-skeleton>
</template>
```

### Round Style

```vue
<template>
  <van-skeleton title avatar :row="3" round />
</template>
```

### Custom Row Width

```vue
<template>
  <van-skeleton :row="5" :row-width="['100%', '60%', '80%', '40%', '100%']" />
</template>
```

### Without Animation

```vue
<template>
  <van-skeleton title :row="3" :animate="false" />
</template>
```

### List Item Skeleton

```vue
<template>
  <div class="list-skeleton">
    <van-skeleton
      v-for="i in 3"
      :key="i"
      title
      avatar
      :row="2"
      :loading="loading"
    >
      <div class="list-item">
        <img :src="items[i - 1]?.avatar" class="avatar" />
        <div class="info">
          <h4>{{ items[i - 1]?.title }}</h4>
          <p>{{ items[i - 1]?.desc }}</p>
        </div>
      </div>
    </van-skeleton>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const loading = ref(true);
const items = ref([]);

onMounted(async () => {
  await fetchData();
  loading.value = false;
});

const fetchData = async () => {
  // Simulate API call
  items.value = [
    { avatar: 'url1', title: 'Title 1', desc: 'Description 1' },
    { avatar: 'url2', title: 'Title 2', desc: 'Description 2' },
    { avatar: 'url3', title: 'Title 3', desc: 'Description 3' },
  ];
};
</script>
```

## Best Practices

1. **Match skeleton to content**: Design skeleton layout that matches actual content structure
2. **Use loading toggle**: Use `loading` prop to seamlessly transition to actual content
3. **Consistent sizing**: Match skeleton sizes to actual content dimensions
4. **Disable animation for static**: Use `animate="false"` for static loading states
5. **Custom templates**: Use template slot for complex layouts
