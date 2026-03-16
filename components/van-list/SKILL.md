---
name: "van-list"
description: "List component for displaying items with infinite scroll and loading states. Invoke when user needs to implement infinite scrolling lists or load-more functionality."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant List Component

A list component to show items and control loading status with infinite scroll support.

## When to Invoke

Invoke this skill when:
- User needs to implement infinite scrolling lists
- User wants to load more data on scroll
- User needs to handle loading, error, and finished states
- User wants to implement pull-to-refresh with lists
- User asks about scroll-based data loading

## Features

- **Infinite Scroll**: Automatic loading when scrolling to bottom
- **Loading States**: Built-in loading, error, and finished states
- **Pull-to-Refresh**: Works with PullRefresh component
- **Custom Offset**: Configurable trigger distance
- **Direction Control**: Support up and down scroll directions
- **Custom Slots**: Customizable loading, error, and finished content
- **Manual Check**: Programmatic scroll position checking

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model:loading | Whether to show loading info | `boolean` | `false` |
| v-model:error | Whether loading is error | `boolean` | `false` |
| finished | Whether loading is finished | `boolean` | `false` |
| offset | Load event trigger distance | `number \| string` | `300` |
| loading-text | Loading text | `string` | `Loading...` |
| finished-text | Finished text | `string` | - |
| error-text | Error loaded text | `string` | - |
| immediate-check | Whether to check immediately after mounted | `boolean` | `true` |
| disabled | Whether to disable the load event | `boolean` | `false` |
| direction | Scroll direction, can be set to `up` | `string` | `down` |
| scroller | Specifies the node for scroll events | `Element` | - |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| load | Emitted when distance to bottom is less than offset | - |

### Methods

| Name | Description | Attribute | Return value |
|------|-------------|-----------|--------------|
| check | Check scroll position | - | - |

### Slots

| Name | Description |
|------|-------------|
| default | List content |
| loading | Custom loading tips |
| finished | Custom finished tips |
| error | Custom error tips |

### Types

```ts
import type { ListProps, ListInstance, ListDirection } from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-list
    v-model:loading="loading"
    :finished="finished"
    finished-text="Finished"
    @load="onLoad"
  >
    <van-cell v-for="item in list" :key="item" :title="item" />
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
      list.value.push(list.value.length + 1);
    }
    loading.value = false;

    if (list.value.length >= 40) {
      finished.value = true;
    }
  }, 1000);
};
</script>
```

### Error Handling

```vue
<template>
  <van-list
    v-model:loading="loading"
    v-model:error="error"
    error-text="Request failed. Click to reload"
    @load="onLoad"
  >
    <van-cell v-for="item in list" :key="item" :title="item" />
  </van-list>
</template>

<script setup>
import { ref } from 'vue';

const list = ref([]);
const error = ref(false);
const loading = ref(false);

const onLoad = async () => {
  try {
    const data = await fetchData();
    list.value.push(...data);
    loading.value = false;
  } catch (e) {
    loading.value = false;
    error.value = true;
  }
};
</script>
```

### With PullRefresh

```vue
<template>
  <van-pull-refresh v-model="refreshing" @refresh="onRefresh">
    <van-list
      v-model:loading="loading"
      :finished="finished"
      finished-text="Finished"
      @load="onLoad"
    >
      <van-cell v-for="item in list" :key="item" :title="item" />
    </van-list>
  </van-pull-refresh>
</template>

<script setup>
import { ref } from 'vue';

const list = ref([]);
const loading = ref(false);
const finished = ref(false);
const refreshing = ref(false);

const onLoad = () => {
  setTimeout(() => {
    if (refreshing.value) {
      list.value = [];
      refreshing.value = false;
    }

    for (let i = 0; i < 10; i++) {
      list.value.push(list.value.length + 1);
    }
    loading.value = false;

    if (list.value.length >= 40) {
      finished.value = true;
    }
  }, 1000);
};

const onRefresh = () => {
  finished.value = false;
  loading.value = true;
  onLoad();
};
</script>
```

### Custom Loading Content

```vue
<template>
  <van-list
    v-model:loading="loading"
    :finished="finished"
    @load="onLoad"
  >
    <van-cell v-for="item in list" :key="item" :title="item" />
    <template #loading>
      <van-loading type="spinner" />
      <span>Loading more...</span>
    </template>
  </van-list>
</template>
```

### Upward Direction

```vue
<template>
  <van-list
    v-model:loading="loading"
    :finished="finished"
    direction="up"
    @load="onLoad"
  >
    <van-cell v-for="item in list" :key="item" :title="item" />
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
      list.value.unshift(list.value.length + 1);
    }
    loading.value = false;

    if (list.value.length >= 40) {
      finished.value = true;
    }
  }, 1000);
};
</script>
```

## Common Issues

### 1. Load Event Triggered Continuously

If loaded data is too small, List will keep triggering. Load enough data to fill the screen:

```js
const onLoad = () => {
  fetchData().then(data => {
    list.value.push(...data);
    loading.value = false;
    // Ensure enough data is loaded
  });
};
```

### 2. Float Layout Issues

Add `van-clearfix` class for float layouts:

```vue
<van-list>
  <div class="van-clearfix">
    <div class="float-item" />
  </div>
</van-list>
```

### 3. Overflow on HTML/Body

Avoid `overflow-x: hidden` on html/body, or add `height: 100%`:

```css
html, body {
  overflow-x: hidden;
  height: 100%;
}
```

### 4. Understanding States

- `loading = false`: Not loading, will trigger load based on scroll
- `loading = true`: Loading, won't trigger load
- `finished = true`: Complete, won't trigger load

Always set `loading = false` after request completes.

## Component Interactions

### With Search

```vue
<template>
  <van-search v-model="keyword" @search="onSearch" />
  <van-list
    v-model:loading="loading"
    :finished="finished"
    @load="onLoad"
  >
    <van-cell 
      v-for="item in list" 
      :key="item.id" 
      :title="item.title" 
    />
  </van-list>
</template>

<script setup>
import { ref } from 'vue';

const keyword = ref('');
const list = ref([]);
const loading = ref(false);
const finished = ref(false);
const page = ref(1);

const onLoad = async () => {
  const data = await fetchData(keyword.value, page.value);
  list.value.push(...data);
  page.value++;
  loading.value = false;
  
  if (data.length < 10) {
    finished.value = true;
  }
};

const onSearch = () => {
  list.value = [];
  page.value = 1;
  finished.value = false;
  onLoad();
};
</script>
```

### With Tabs

```vue
<template>
  <van-tabs v-model:active="activeTab">
    <van-tab title="All">
      <van-list v-model:loading="loading" :finished="finished" @load="onLoad">
        <van-cell v-for="item in list" :key="item.id" :title="item.title" />
      </van-list>
    </van-tab>
  </van-tabs>
</template>
```

## Best Practices

1. **Load enough data**: Ensure each load fills at least one screen
2. **Handle errors gracefully**: Provide retry options for failed loads
3. **Reset state properly**: Reset loading and finished states when filtering
4. **Use appropriate offset**: Adjust offset based on your layout
5. **Test on slow networks**: Verify behavior on slow connections
