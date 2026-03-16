---
name: "van-loading"
description: "Loading component for displaying loading states and spinners. Invoke when user needs to implement loading indicators, loading overlays, or progress feedback."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Loading Component

A loading indicator component used to show transition states during loading operations.

## When to Invoke

Invoke this skill when:
- User needs to display a loading indicator
- User wants to show loading state during async operations
- User needs to implement loading overlays
- User asks about spinner types or loading animations
- User wants to customize loading appearance

## Features

- **Two Types**: Circular and spinner animations
- **Custom Colors**: Configurable icon and text colors
- **Size Control**: Adjustable icon and text sizes
- **Text Support**: Display loading text alongside spinner
- **Vertical Layout**: Option for vertical arrangement
- **Custom Icon**: Slot for custom loading icons

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| color | Loading color | `string` | `#c9c9c9` |
| type | Can be set to `spinner` | `string` | `circular` |
| size | Icon size | `number \| string` | `30px` |
| text-size | Text font size | `number \| string` | `14px` |
| text-color | Text color | `string` | `#c9c9c9` |
| vertical | Whether to arrange icons and text vertically | `boolean` | `false` |

### Slots

| Name | Description |
|------|-------------|
| default | Loading text |
| icon | Custom loading icon |

### Types

```ts
import type { LoadingType, LoadingProps } from 'vant'
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-loading />
</template>
```

### Spinner Type

```vue
<template>
  <van-loading type="spinner" />
</template>
```

### Custom Color

```vue
<template>
  <van-loading color="#1989fa" />
  <van-loading type="spinner" color="#1989fa" />
</template>
```

### Custom Size

```vue
<template>
  <van-loading size="24" />
  <van-loading type="spinner" size="24px" />
</template>
```

### With Text

```vue
<template>
  <van-loading size="24px">Loading...</van-loading>
</template>
```

### Vertical Layout

```vue
<template>
  <van-loading size="24px" vertical>Loading...</van-loading>
</template>
```

### Separate Text Color

```vue
<template>
  <van-loading color="#0094ff" />
  <van-loading text-color="#0094ff">Loading...</van-loading>
</template>
```

### Custom Icon

```vue
<template>
  <van-loading vertical>
    <template #icon>
      <van-icon name="star-o" size="30" />
    </template>
    Loading...
  </van-loading>
</template>
```

## Common Issues

### 1. Loading Not Centered

Wrap in a flex container:

```vue
<template>
  <div style="display: flex; justify-content: center; align-items: center; height: 100px;">
    <van-loading />
  </div>
</template>
```

### 2. Different Text and Icon Colors

Use separate `color` and `text-color` props:

```vue
<van-loading color="#1989fa" text-color="#333">Loading...</van-loading>
```

### 3. Loading Overlay

Combine with Overlay component:

```vue
<template>
  <van-overlay :show="loading">
    <div class="loading-wrapper">
      <van-loading type="spinner" color="#fff" />
    </div>
  </van-overlay>
</template>

<style scoped>
.loading-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}
</style>
```

## Component Interactions

### With Button Loading State

```vue
<template>
  <van-button :loading="submitting" @click="handleSubmit">
    {{ submitting ? 'Submitting...' : 'Submit' }}
  </van-button>
</template>

<script setup>
import { ref } from 'vue'

const submitting = ref(false)

const handleSubmit = async () => {
  submitting.value = true
  try {
    await submitData()
  } finally {
    submitting.value = false
  }
}
</script>
```

### With List Loading

```vue
<template>
  <van-list v-model:loading="loading" :finished="finished" @load="onLoad">
    <van-cell v-for="item in list" :key="item.id" :title="item.title" />
    <template #loading>
      <van-loading type="spinner" size="20" />
    </template>
  </van-list>
</template>
```

### With Page Loading

```vue
<template>
  <div v-if="loading" class="page-loading">
    <van-loading size="36px" vertical>Loading page...</van-loading>
  </div>
  <div v-else>
    <!-- Page content -->
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const loading = ref(true)

onMounted(async () => {
  await fetchData()
  loading.value = false
})
</script>

<style scoped>
.page-loading {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
</style>
```

### With Pull Refresh

```vue
<template>
  <van-pull-refresh v-model="refreshing" @refresh="onRefresh">
    <van-list v-model:loading="loading" :finished="finished" @load="onLoad">
      <van-cell v-for="item in list" :key="item.id" :title="item.title" />
    </van-list>
  </van-pull-refresh>
</template>
```

## Best Practices

1. **Consistent styling**: Use consistent colors matching your theme
2. **Appropriate size**: Use larger sizes for full-page loading
3. **Text feedback**: Add descriptive text for longer operations
4. **Type selection**: Use `spinner` for simpler interfaces
5. **Accessibility**: Provide aria-label for screen readers
6. **Performance**: Hide loading when operation completes
