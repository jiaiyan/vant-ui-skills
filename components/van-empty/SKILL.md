---
name: "van-empty"
description: "Empty state component for displaying placeholder content when no data is available. Invoke when user needs to show empty states, error pages, or placeholder illustrations."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Empty Component

Occupation reminder when empty, used to display placeholder content when no data is available.

## When to Invoke

Invoke this skill when:
- User needs to display empty state placeholders
- User wants to show error pages or network errors
- User needs to indicate no search results
- User wants to customize empty state illustrations
- User asks about placeholder images for different scenarios

## Features

- **Multiple Image Types**: Default, error, network, search images
- **Custom Images**: Support custom image URLs
- **Size Control**: Adjustable image size
- **Custom Description**: Flexible description text
- **Bottom Content**: Support custom bottom content via slots
- **Custom Slots**: Full customization of image and description

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| image | Image type, can be set to `error` `network` `search` or image URL | `string` | `default` |
| image-size | Image size | `number \| string \| Array` | - |
| description | Description | `string` | - |

### Slots

| Name | Description |
|------|-------------|
| default | Custom bottom content |
| image | Custom image |
| description | Custom description |

### Types

```ts
import type { EmptyProps } from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-empty description="Description" />
</template>
```

### Image Types

```vue
<template>
  <van-empty image="error" description="Error occurred" />
  <van-empty image="network" description="Network error" />
  <van-empty image="search" description="No results found" />
</template>
```

### Custom Size

```vue
<template>
  <van-empty image-size="100" description="Description" />
  <van-empty image-size="10rem" description="Description" />
</template>
```

### Separate Width and Height

```vue
<template>
  <van-empty :image-size="[60, 40]" description="Description" />
</template>
```

### Custom Image

```vue
<template>
  <van-empty
    image="https://fastly.jsdelivr.net/npm/@vant/assets/leaf.jpeg"
    image-size="80"
    description="Description"
  />
</template>
```

### Bottom Content

```vue
<template>
  <van-empty description="Description">
    <van-button round type="primary" class="bottom-button">Button</van-button>
  </van-empty>
</template>

<style scoped>
.bottom-button {
  width: 160px;
  height: 40px;
}
</style>
```

### Custom Image Slot

```vue
<template>
  <van-empty description="No data">
    <template #image>
      <van-icon name="info-o" size="80" color="#969799" />
    </template>
  </van-empty>
</template>
```

### Custom Description Slot

```vue
<template>
  <van-empty>
    <template #description>
      <p>Custom description with <span style="color: #1989fa;">highlighted text</span></p>
    </template>
  </van-empty>
</template>
```

## Common Issues

### 1. Image Not Loading

Ensure the image URL is accessible and properly formatted:

```vue
<van-empty
  image="https://example.com/image.png"
  description="Description"
/>
```

### 2. Custom Size Not Working

Use proper format for image-size:

```vue
<van-empty image-size="100" />
<van-empty :image-size="100" />
<van-empty :image-size="[100, 80]" />
```

### 3. Bottom Content Alignment

Bottom content is centered by default. Use CSS to adjust:

```vue
<van-empty description="Description">
  <van-button style="margin-top: 20px;">Action</van-button>
</van-empty>
```

## Component Interactions

### With List Component

```vue
<template>
  <van-list v-if="list.length > 0">
    <van-cell v-for="item in list" :key="item.id" :title="item.title" />
  </van-list>
  <van-empty v-else description="No data available" />
</template>

<script setup>
import { ref } from 'vue';

const list = ref([]);
</script>
```

### With Search Results

```vue
<template>
  <div v-if="searchResults.length > 0">
    <van-cell 
      v-for="result in searchResults" 
      :key="result.id"
      :title="result.title"
    />
  </div>
  <van-empty 
    v-else 
    image="search" 
    description="No results found"
  >
    <van-button type="primary" size="small" @click="clearSearch">
      Clear Search
    </van-button>
  </van-empty>
</template>

<script setup>
import { ref } from 'vue';

const searchResults = ref([]);

const clearSearch = () => {
  console.log('Clear search');
};
</script>
```

### With Error Handling

```vue
<template>
  <van-empty 
    v-if="error" 
    image="error" 
    :description="errorMessage"
  >
    <van-button type="primary" @click="retry">Retry</van-button>
  </van-empty>
  <div v-else>
    <!-- Normal content -->
  </div>
</template>

<script setup>
import { ref } from 'vue';

const error = ref(false);
const errorMessage = ref('Something went wrong');

const retry = () => {
  error.value = false;
  // Retry logic
};
</script>
```

### With Network Status

```vue
<template>
  <van-empty 
    v-if="!isOnline" 
    image="network" 
    description="No internet connection"
  >
    <van-button type="primary" @click="checkConnection">
      Check Connection
    </van-button>
  </van-empty>
</template>

<script setup>
import { ref } from 'vue';

const isOnline = ref(navigator.onLine);

const checkConnection = () => {
  isOnline.value = navigator.onLine;
};
</script>
```

## Best Practices

1. **Use appropriate image types**: Match image type to the context (error, network, search)
2. **Provide clear description**: Make sure users understand why the content is empty
3. **Offer actions**: Provide actionable buttons when appropriate
4. **Consistent styling**: Use consistent empty state styling throughout the app
5. **Accessibility**: Ensure empty states are accessible to screen readers
