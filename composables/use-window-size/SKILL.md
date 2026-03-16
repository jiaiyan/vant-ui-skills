---
name: "use-window-size"
description: "Composable for tracking browser window dimensions. Invoke when implementing responsive designs, layouts that adapt to window size, or components that need window dimensions."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# useWindowSize

A Vue 3 composable that gets the viewport width and height of the browser window, automatically updating when the window is resized.

## When to Invoke

Invoke this skill when:
- User needs to implement responsive layouts
- User wants to track window size changes
- User needs to conditionally render based on screen size
- User wants to implement breakpoints in Vue
- User needs to calculate element sizes based on window

## Features

- **Reactive**: Width and height update automatically on resize
- **Debounced**: Updates are optimized for performance
- **Simple API**: Returns width and height as refs
- **Watch Support**: Can be watched for size changes
- **TypeScript Support**: Full TypeScript type definitions

## API Reference

### Type Declarations

```ts
function useWindowSize(): {
  width: Ref<number>;
  height: Ref<number>;
};
```

### Return Value

| Name | Description | Type |
| --- | --- | --- |
| width | The width of the browser window | `Ref<number>` |
| height | The height of the browser window | `Ref<number>` |

## Usage Examples

### Basic Usage

```vue
<template>
  <div>
    <p>Window width: {{ width }}px</p>
    <p>Window height: {{ height }}px</p>
  </div>
</template>

<script setup>
import { useWindowSize } from '@vant/use';

const { width, height } = useWindowSize();
</script>
```

### Responsive Breakpoints

```vue
<template>
  <div :class="deviceClass">
    <p>Current device: {{ deviceType }}</p>
    <p>Window size: {{ width }} x {{ height }}</p>
  </div>
</template>

<script setup>
import { computed } from 'vue';
import { useWindowSize } from '@vant/use';

const { width, height } = useWindowSize();

const deviceType = computed(() => {
  if (width.value < 576) return 'mobile';
  if (width.value < 768) return 'tablet';
  if (width.value < 992) return 'laptop';
  return 'desktop';
});

const deviceClass = computed(() => `device-${deviceType.value}`);
</script>

<style scoped>
.device-mobile { background: #ffebee; }
.device-tablet { background: #e8f5e9; }
.device-laptop { background: #e3f2fd; }
.device-desktop { background: #fff3e0; }
</style>
```

### Conditional Rendering

```vue
<template>
  <div>
    <div v-if="isMobile" class="mobile-view">
      <p>Mobile optimized view</p>
    </div>
    <div v-else class="desktop-view">
      <p>Desktop optimized view</p>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue';
import { useWindowSize } from '@vant/use';

const { width } = useWindowSize();

const isMobile = computed(() => width.value < 768);
</script>
```

### Watch Size Changes

```vue
<template>
  <div>
    <p>Window size: {{ width }} x {{ height }}</p>
    <p>Resize count: {{ resizeCount }}</p>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';
import { useWindowSize } from '@vant/use';

const { width, height } = useWindowSize();
const resizeCount = ref(0);

watch([width, height], () => {
  resizeCount.value++;
  console.log('Window resized');
});
</script>
```

### Grid Layout Adjustment

```vue
<template>
  <div class="grid" :style="gridStyle">
    <div v-for="i in 12" :key="i" class="grid-item">
      {{ i }}
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue';
import { useWindowSize } from '@vant/use';

const { width } = useWindowSize();

const columns = computed(() => {
  if (width.value < 576) return 2;
  if (width.value < 768) return 3;
  if (width.value < 992) return 4;
  return 6;
});

const gridStyle = computed(() => ({
  gridTemplateColumns: `repeat(${columns.value}, 1fr)`,
}));
</script>

<style scoped>
.grid {
  display: grid;
  gap: 16px;
  padding: 16px;
}

.grid-item {
  background: #409eff;
  color: white;
  padding: 20px;
  text-align: center;
  border-radius: 4px;
}
</style>
```

### Aspect Ratio Calculation

```vue
<template>
  <div>
    <p>Window aspect ratio: {{ aspectRatio.toFixed(2) }}</p>
    <p>Orientation: {{ orientation }}</p>
  </div>
</template>

<script setup>
import { computed } from 'vue';
import { useWindowSize } from '@vant/use';

const { width, height } = useWindowSize();

const aspectRatio = computed(() => width.value / height.value);

const orientation = computed(() => {
  return width.value > height.value ? 'Landscape' : 'Portrait';
});
</script>
```

### Sidebar Visibility

```vue
<template>
  <div class="layout">
    <aside v-show="showSidebar" class="sidebar">
      <nav>Sidebar Navigation</nav>
    </aside>
    <main class="content">
      <button v-if="!showSidebar" @click="toggleSidebar">
        Show Sidebar
      </button>
      <p>Main content</p>
    </main>
  </div>
</template>

<script setup>
import { ref, computed, watch } from 'vue';
import { useWindowSize } from '@vant/use';

const { width } = useWindowSize();
const sidebarVisible = ref(true);

const showSidebar = computed(() => {
  return width.value >= 768 ? true : sidebarVisible.value;
});

const toggleSidebar = () => {
  sidebarVisible.value = !sidebarVisible.value;
};

watch(width, (newWidth) => {
  if (newWidth >= 768) {
    sidebarVisible.value = true;
  }
});
</script>

<style scoped>
.layout {
  display: flex;
  min-height: 100vh;
}

.sidebar {
  width: 250px;
  background: #333;
  color: white;
  padding: 16px;
}

.content {
  flex: 1;
  padding: 16px;
}
</style>
```

### Full Screen Component

```vue
<template>
  <div class="fullscreen" :style="fullScreenStyle">
    <p>Window: {{ width }} x {{ height }}</p>
    <slot />
  </div>
</template>

<script setup>
import { computed } from 'vue';
import { useWindowSize } from '@vant/use';

const { width, height } = useWindowSize();

const fullScreenStyle = computed(() => ({
  width: `${width.value}px`,
  height: `${height.value}px`,
}));
</script>

<style scoped>
.fullscreen {
  overflow: hidden;
}
</style>
```

### Responsive Font Size

```vue
<template>
  <div :style="{ fontSize: fontSize + 'px' }">
    <h1>Responsive Title</h1>
    <p>This text scales with window width</p>
  </div>
</template>

<script setup>
import { computed } from 'vue';
import { useWindowSize } from '@vant/use';

const { width } = useWindowSize();

const fontSize = computed(() => {
  const baseSize = 16;
  const scale = width.value / 1920;
  return Math.max(12, Math.min(24, baseSize * scale));
});
</script>
```

## Best Practices

1. **Debounce**: The composable handles debouncing internally
2. **Breakpoints**: Define breakpoint constants for consistency
3. **Computed**: Use computed for derived values like device type
4. **Watch**: Watch width/height for side effects
5. **Mobile First**: Design for mobile and enhance for larger screens
