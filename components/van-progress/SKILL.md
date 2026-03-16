---
name: "van-progress"
description: "Progress bar component for displaying operation progress. Invoke when user needs to show linear progress indicators for tasks, uploads, or downloads."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Progress Component

Used to show the current progress of the operation.

## When to Invoke

Invoke this skill when:
- User needs to display linear progress bars
- User wants to show upload or download progress
- User needs to indicate task completion status
- User wants to customize progress bar appearance
- User asks about progress bar styling and colors

## Features

- **Percentage Display**: Show progress as percentage
- **Custom Stroke Width**: Adjustable bar thickness
- **Color Customization**: Custom colors and gradients
- **Inactive State**: Grayed out for inactive progress
- **Custom Pivot**: Custom text and styling for pivot
- **Pivot Slot**: Full customization of pivot content
- **Track Color**: Custom background track color

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| percentage | Percentage | `number \| string` | `0` |
| stroke-width | Stroke width | `number \| string` | `4px` |
| color | Color | `string` | `#1989fa` |
| track-color | Track color | `string` | `#e5e5e5` |
| pivot-text | Pivot text | `string` | percentage |
| pivot-color | Pivot text background color | `string` | inherit progress color |
| text-color | Pivot text color | `string` | `white` |
| inactive | Whether to be gray | `boolean` | `false` |
| show-pivot | Whether to show text | `boolean` | `true` |

### Slots

| Name | Description | SlotProps |
|------|-------------|-----------|
| pivot | Custom pivot content | `{ percentage: number }` |

### Types

```ts
import type { ProgressProps, ProgressInstance } from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-progress :percentage="50" />
</template>
```

### Stroke Width

```vue
<template>
  <van-progress :percentage="50" stroke-width="8" />
</template>
```

### Inactive State

```vue
<template>
  <van-progress inactive :percentage="50" />
</template>
```

### Custom Style

```vue
<template>
  <van-progress pivot-text="Orange" color="#f2826a" :percentage="25" />
  <van-progress pivot-text="Red" color="#ee0a24" :percentage="50" />
  <van-progress
    :percentage="75"
    pivot-text="Purple"
    pivot-color="#7232dd"
    color="linear-gradient(to right, #be99ff, #7232dd)"
  />
</template>
```

### Custom Pivot Content

```vue
<template>
  <van-progress :percentage="50">
    <template #pivot="{ percentage }">
      <van-icon name="fire" />
      <span>{{ percentage }}%</span>
    </template>
  </van-progress>
</template>
```

### Without Pivot

```vue
<template>
  <van-progress :percentage="50" :show-pivot="false" />
</template>
```

### Gradient Color

```vue
<template>
  <van-progress
    :percentage="70"
    color="linear-gradient(to right, #be99ff, #7232dd)"
  />
</template>
```

### Custom Track Color

```vue
<template>
  <van-progress
    :percentage="50"
    track-color="#f5f5f5"
    color="#1989fa"
  />
</template>
```

## Common Issues

### 1. Pivot Text Not Showing

Ensure `show-pivot` is not set to `false`:

```vue
<van-progress :percentage="50" :show-pivot="true" />
```

### 2. Custom Color Not Working

Use valid CSS color values:

```vue
<van-progress :percentage="50" color="#1989fa" />
<van-progress :percentage="50" color="rgb(25, 137, 250)" />
<van-progress :percentage="50" color="linear-gradient(to right, #be99ff, #7232dd)" />
```

### 3. Percentage Out of Range

Ensure percentage is between 0 and 100:

```vue
<van-progress :percentage="Math.min(100, Math.max(0, value))" />
```

## Component Interactions

### With Upload Progress

```vue
<template>
  <div class="upload-item">
    <span>Uploading...</span>
    <van-progress
      :percentage="uploadProgress"
      stroke-width="6"
      color="#1989fa"
    />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const uploadProgress = ref(0);

onMounted(() => {
  const timer = setInterval(() => {
    uploadProgress.value += 10;
    if (uploadProgress.value >= 100) {
      clearInterval(timer);
    }
  }, 500);
});
</script>
```

### With Multiple Progress Bars

```vue
<template>
  <div class="progress-list">
    <div class="progress-item">
      <span>Download</span>
      <van-progress :percentage="downloadProgress" color="#07c160" />
    </div>
    <div class="progress-item">
      <span>Upload</span>
      <van-progress :percentage="uploadProgress" color="#1989fa" />
    </div>
    <div class="progress-item">
      <span>Process</span>
      <van-progress :percentage="processProgress" color="#ff976a" />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const downloadProgress = ref(80);
const uploadProgress = ref(60);
const processProgress = ref(40);
</script>

<style scoped>
.progress-item {
  margin-bottom: 16px;
}
</style>
```

### With Task Status

```vue
<template>
  <van-cell-group>
    <van-cell v-for="task in tasks" :key="task.id" :title="task.name">
      <template #value>
        <van-progress
          :percentage="task.progress"
          :color="task.status === 'error' ? '#ee0a24' : '#1989fa'"
          :inactive="task.status === 'paused'"
          stroke-width="4"
        />
      </template>
    </van-cell>
  </van-cell-group>
</template>

<script setup>
import { ref } from 'vue';

const tasks = ref([
  { id: 1, name: 'Task 1', progress: 80, status: 'running' },
  { id: 2, name: 'Task 2', progress: 50, status: 'paused' },
  { id: 3, name: 'Task 3', progress: 30, status: 'error' },
]);
</script>
```

### With Animated Progress

```vue
<template>
  <van-button @click="startProgress">Start</van-button>
  <van-progress :percentage="progress" :stroke-width="8" />
</template>

<script setup>
import { ref } from 'vue';

const progress = ref(0);

const startProgress = () => {
  progress.value = 0;
  const timer = setInterval(() => {
    progress.value += 5;
    if (progress.value >= 100) {
      progress.value = 100;
      clearInterval(timer);
    }
  }, 100);
};
</script>
```

## Best Practices

1. **Use appropriate stroke width**: Thicker bars for important progress, thinner for subtle indicators
2. **Provide context**: Add labels or descriptions to explain what the progress represents
3. **Use semantic colors**: Green for success, red for errors, blue for in-progress
4. **Keep percentage accurate**: Ensure percentage reflects actual progress
5. **Consider accessibility**: Ensure sufficient color contrast for visibility
