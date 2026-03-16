---
name: "use-page-visibility"
description: "Composable for tracking page visibility state. Invoke when detecting if the page is visible or hidden, useful for pausing animations or media when tab is inactive."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# usePageVisibility

A Vue 3 composable that tracks the visibility state of the page, detecting when the user switches tabs or minimizes the browser window.

## When to Invoke

Invoke this skill when:
- User needs to pause video/audio when tab is hidden
- User wants to stop animations when page is not visible
- User needs to save data when user leaves the page
- User wants to track user engagement and attention
- User needs to pause polling or background tasks

## Features

- **Real-time Tracking**: Reactively tracks page visibility state
- **Simple API**: Returns a single ref with 'visible' or 'hidden' state
- **Watch Support**: Can be watched for state changes
- **Performance Optimization**: Helps optimize resource usage
- **TypeScript Support**: Full TypeScript type definitions

## API Reference

### Type Declarations

```ts
type VisibilityState = 'visible' | 'hidden';

function usePageVisibility(): Ref<VisibilityState>;
```

### Return Value

| Name | Description | Type |
| --- | --- | --- |
| visibilityState | Current visibility state ('visible' or 'hidden') | `Ref<VisibilityState>` |

## Usage Examples

### Basic Usage

```vue
<template>
  <div>
    <p>Page is: {{ pageVisibility }}</p>
  </div>
</template>

<script setup>
import { usePageVisibility } from '@vant/use';

const pageVisibility = usePageVisibility();
</script>
```

### Pause Video When Hidden

```vue
<template>
  <div>
    <video ref="videoRef" src="video.mp4" controls />
    <p v-if="pageVisibility === 'hidden'">Video paused (tab inactive)</p>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';
import { usePageVisibility } from '@vant/use';

const videoRef = ref();
const pageVisibility = usePageVisibility();

watch(pageVisibility, (visibility) => {
  if (videoRef.value) {
    if (visibility === 'hidden') {
      videoRef.value.pause();
    } else {
      videoRef.value.play();
    }
  }
});
</script>
```

### Stop Animation When Hidden

```vue
<template>
  <div class="animation-container">
    <div class="animated-box" :class="{ paused: pageVisibility === 'hidden' }" />
  </div>
</template>

<script setup>
import { usePageVisibility } from '@vant/use';

const pageVisibility = usePageVisibility();
</script>

<style scoped>
.animated-box {
  width: 100px;
  height: 100px;
  background: linear-gradient(45deg, #409eff, #67c23a);
  animation: rotate 2s linear infinite;
}

.animated-box.paused {
  animation-play-state: paused;
}

@keyframes rotate {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}
</style>
```

### Pause Polling When Hidden

```vue
<template>
  <div>
    <p>Polling status: {{ isPolling ? 'Active' : 'Paused' }}</p>
    <p>Data updates: {{ updateCount }}</p>
  </div>
</template>

<script setup>
import { ref, watch, onUnmounted } from 'vue';
import { usePageVisibility } from '@vant/use';

const pageVisibility = usePageVisibility();
const isPolling = ref(true);
const updateCount = ref(0);
let intervalId = null;

const startPolling = () => {
  intervalId = setInterval(() => {
    updateCount.value++;
    console.log('Polling data...');
  }, 1000);
  isPolling.value = true;
};

const stopPolling = () => {
  if (intervalId) {
    clearInterval(intervalId);
    intervalId = null;
  }
  isPolling.value = false;
};

watch(pageVisibility, (visibility) => {
  if (visibility === 'hidden') {
    stopPolling();
  } else {
    startPolling();
  }
});

startPolling();

onUnmounted(() => {
  stopPolling();
});
</script>
```

### Save Data on Page Hide

```vue
<template>
  <div>
    <textarea v-model="content" placeholder="Type something..." />
    <p v-if="saved">Auto-saved!</p>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';
import { usePageVisibility } from '@vant/use';

const content = ref('');
const saved = ref(false);

const pageVisibility = usePageVisibility();

const saveData = async () => {
  if (content.value) {
    await fetch('/api/save', {
      method: 'POST',
      body: JSON.stringify({ content: content.value }),
    });
    saved.value = true;
    setTimeout(() => {
      saved.value = false;
    }, 2000);
  }
};

watch(pageVisibility, (visibility) => {
  if (visibility === 'hidden') {
    saveData();
  }
});
</script>
```

### Track User Engagement

```vue
<template>
  <div>
    <p>Active time: {{ formatTime(activeTime) }}</p>
    <p>Total time: {{ formatTime(totalTime) }}</p>
  </div>
</template>

<script setup>
import { ref, watch, onUnmounted } from 'vue';
import { usePageVisibility } from '@vant/use';

const pageVisibility = usePageVisibility();
const activeTime = ref(0);
const totalTime = ref(0);
let intervalId = null;

const formatTime = (seconds) => {
  const mins = Math.floor(seconds / 60);
  const secs = seconds % 60;
  return `${mins}m ${secs}s`;
};

intervalId = setInterval(() => {
  totalTime.value++;
  if (pageVisibility.value === 'visible') {
    activeTime.value++;
  }
}, 1000);

onUnmounted(() => {
  if (intervalId) {
    clearInterval(intervalId);
  }
});
</script>
```

### Combined with Other Composables

```vue
<template>
  <div>
    <p>Visibility: {{ pageVisibility }}</p>
    <p>Window size: {{ width }} x {{ height }}</p>
  </div>
</template>

<script setup>
import { watch } from 'vue';
import { usePageVisibility, useWindowSize } from '@vant/use';

const pageVisibility = usePageVisibility();
const { width, height } = useWindowSize();

watch(pageVisibility, (visibility) => {
  console.log(`Page is now ${visibility} at ${width.value}x${height.value}`);
});
</script>
```

## Best Practices

1. **Resource Optimization**: Pause expensive operations when page is hidden
2. **User Experience**: Don't interrupt user when they return to the page
3. **Battery Saving**: Stop animations and media to save battery on mobile
4. **Data Conservation**: Pause non-essential network requests
5. **Analytics**: Track visibility changes for engagement metrics
