---
name: "van-pull-refresh"
description: "Pull refresh component for implementing pull-to-refresh functionality. Invoke when user needs to implement list refresh, page refresh, or pull-down loading interactions."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant PullRefresh Component

A component for providing pull-down refresh interactions, commonly used to refresh list data.

## When to Invoke

Invoke this skill when:
- User needs to implement pull-to-refresh functionality
- User wants to refresh list data on pull down
- User needs custom pull-down animations
- User asks about mobile refresh patterns
- User wants to implement refresh indicators

## Features

- **Pull Detection**: Detect pull-down gestures
- **Custom Text**: Configurable text for different states
- **Success Feedback**: Optional success message
- **Custom Slots**: Fully customizable pull indicators
- **Disabled State**: Option to disable pull refresh
- **Distance Control**: Configurable trigger distance

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model | Loading status | `boolean` | - |
| pulling-text | Text when pulling | `string` | `Pull to refresh...` |
| loosing-text | Text when loosing | `string` | `Loose to refresh...` |
| loading-text | Text when loading | `string` | `Loading...` |
| success-text | Text on success | `string` | - |
| success-duration | Success text display duration(ms) | `number \| string` | `500` |
| animation-duration | Animation duration | `number \| string` | `300` |
| head-height | Height of head | `number \| string` | `50` |
| pull-distance | Distance to trigger refresh | `number \| string` | same as head-height |
| disabled | Whether to disable pull refresh | `boolean` | `false` |

### Events

| Event | Description | Parameters |
|-------|-------------|------------|
| refresh | Emitted after pulling refresh | - |
| change | Emitted when dragging or status changed | `{ status: string, distance: number }` |

### Slots

| Name | Description | SlotProps |
|------|-------------|-----------|
| default | Default slot | - |
| normal | Content of head at normal status | - |
| pulling | Content of head when pulling | `{ distance: number }` |
| loosing | Content of head when loosing | `{ distance: number }` |
| loading | Content of head when loading | `{ distance: number }` |
| success | Content of head when succeed | - |

### Types

```ts
import type { PullRefreshProps } from 'vant'
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-pull-refresh v-model="loading" @refresh="onRefresh">
    <p>Refresh Count: {{ count }}</p>
  </van-pull-refresh>
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const count = ref(0)
const loading = ref(false)

const onRefresh = () => {
  setTimeout(() => {
    showToast('Refresh Success')
    loading.value = false
    count.value++
  }, 1000)
}
</script>
```

### With Success Text

```vue
<template>
  <van-pull-refresh
    v-model="loading"
    success-text="Refresh success"
    @refresh="onRefresh"
  >
    <p>Refresh Count: {{ count }}</p>
  </van-pull-refresh>
</template>

<script setup>
import { ref } from 'vue'

const count = ref(0)
const loading = ref(false)

const onRefresh = () => {
  setTimeout(() => {
    loading.value = false
    count.value++
  }, 1000)
}
</script>
```

### Custom Indicators

```vue
<template>
  <van-pull-refresh v-model="loading" :head-height="80" @refresh="onRefresh">
    <template #pulling="{ distance }">
      <img
        class="doge"
        src="https://fastly.jsdelivr.net/npm/@vant/assets/doge.png"
        :style="{ transform: `scale(${distance / 80})` }"
      />
    </template>

    <template #loosing>
      <img class="doge" src="https://fastly.jsdelivr.net/npm/@vant/assets/doge.png" />
    </template>

    <template #loading>
      <img class="doge" src="https://fastly.jsdelivr.net/npm/@vant/assets/doge-fire.jpeg" />
    </template>

    <p>Refresh Count: {{ count }}</p>
  </van-pull-refresh>
</template>

<style scoped>
.doge {
  width: 140px;
  height: 72px;
  margin-top: 8px;
  border-radius: 4px;
}
</style>
```

### With List Component

```vue
<template>
  <van-pull-refresh v-model="refreshing" @refresh="onRefresh">
    <van-list
      v-model:loading="loading"
      :finished="finished"
      finished-text="No more"
      @load="onLoad"
    >
      <van-cell v-for="item in list" :key="item.id" :title="item.title" />
    </van-list>
  </van-pull-refresh>
</template>

<script setup>
import { ref } from 'vue'

const list = ref([])
const loading = ref(false)
const finished = ref(false)
const refreshing = ref(false)

const onLoad = () => {
  setTimeout(() => {
    for (let i = 0; i < 10; i++) {
      list.value.push({ id: list.value.length + 1, title: `Item ${list.value.length + 1}` })
    }
    loading.value = false
    if (list.value.length >= 40) {
      finished.value = true
    }
  }, 1000)
}

const onRefresh = () => {
  setTimeout(() => {
    list.value = []
    finished.value = false
    refreshing.value = false
    onLoad()
  }, 1000)
}
</script>
```

## Common Issues

### 1. Refresh Not Triggering

Ensure `v-model` is properly bound and reset after refresh:

```vue
<van-pull-refresh v-model="loading" @refresh="onRefresh">
  <!-- content -->
</van-pull-refresh>

<script setup>
const loading = ref(false)

const onRefresh = async () => {
  await fetchData()
  loading.value = false // Must reset to false
}
</script>
```

### 2. Custom Pull Distance

Adjust `pull-distance` and `head-height`:

```vue
<van-pull-refresh 
  v-model="loading" 
  :head-height="80"
  :pull-distance="100"
  @refresh="onRefresh"
>
  <!-- content -->
</van-pull-refresh>
```

### 3. Disable in Certain Conditions

Use `disabled` prop:

```vue
<van-pull-refresh v-model="loading" :disabled="!canRefresh">
  <!-- content -->
</van-pull-refresh>
```

## Component Interactions

### With Tab Switching

```vue
<template>
  <van-tabs v-model:active="activeTab">
    <van-tab title="All">
      <van-pull-refresh v-model="refreshing" @refresh="onRefresh">
        <van-list v-model:loading="loading" :finished="finished" @load="onLoad">
          <van-cell v-for="item in list" :key="item.id" :title="item.title" />
        </van-list>
      </van-pull-refresh>
    </van-tab>
  </van-tabs>
</template>
```

### With Empty State

```vue
<template>
  <van-pull-refresh v-model="loading" @refresh="onRefresh">
    <van-empty v-if="list.length === 0" description="No data" />
    <van-cell-group v-else>
      <van-cell v-for="item in list" :key="item.id" :title="item.title" />
    </van-cell-group>
  </van-pull-refresh>
</template>
```

### With Error Handling

```vue
<template>
  <van-pull-refresh 
    v-model="loading" 
    success-text="Refresh success"
    @refresh="onRefresh"
  >
    <div v-if="error" class="error-state">
      <p>Load failed</p>
      <van-button @click="onRefresh">Retry</van-button>
    </div>
    <van-list v-else v-model:loading="listLoading" :finished="finished" @load="onLoad">
      <van-cell v-for="item in list" :key="item.id" :title="item.title" />
    </van-list>
  </van-pull-refresh>
</template>

<script setup>
import { ref } from 'vue'

const error = ref(false)

const onRefresh = async () => {
  try {
    await fetchData()
    error.value = false
  } catch (e) {
    error.value = true
  } finally {
    loading.value = false
  }
}
</script>
```

## Best Practices

1. **Reset loading state**: Always set `loading` to `false` after refresh
2. **Success feedback**: Use `success-text` for user confirmation
3. **Custom distance**: Adjust `head-height` for custom indicators
4. **Combine with List**: Use with van-list for complete refresh/load more
5. **Error handling**: Handle errors gracefully in refresh callback
6. **Performance**: Avoid heavy operations during pull animation
