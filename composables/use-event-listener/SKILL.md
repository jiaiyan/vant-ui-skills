---
name: "use-event-listener"
description: "Composable for attaching and automatically removing event listeners. Invoke when adding window, document, or element event listeners with automatic cleanup."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# useEventListener

A Vue 3 composable that automatically handles event listener lifecycle - attaching on mount/activate and removing on unmount/deactivate.

## When to Invoke

Invoke this skill when:
- User needs to add event listeners to window, document, or elements
- User wants automatic cleanup of event listeners
- User needs to handle resize, scroll, or keyboard events
- User wants event listeners that respect component lifecycle
- User needs to attach events to specific elements

## Features

- **Automatic Lifecycle Management**: Attaches on mount/activate, removes on unmount/deactivate
- **Flexible Target**: Support for window, document, or any element
- **Manual Cleanup**: Returns a cleanup function for early removal
- **Options Support**: Supports capture and passive event options
- **Reactive Target**: Target can be a ref that updates dynamically
- **TypeScript Support**: Full TypeScript type definitions

## API Reference

### Type Declarations

```ts
type Options = {
  target?: EventTarget | Ref<EventTarget>;
  capture?: boolean;
  passive?: boolean;
};

function useEventListener(
  type: string,
  listener: EventListener,
  options?: Options,
): () => void;
```

### Parameters

| Name | Description | Type | Default Value |
| --- | --- | --- | --- |
| type | Event type (e.g., 'click', 'resize', 'scroll') | `string` | - |
| listener | Event callback function | `EventListener` | - |
| options | Configuration options | `Options` | - |

### Options

| Name | Description | Type | Default Value |
| --- | --- | --- | --- |
| target | Target element to attach listener to | `EventTarget \| Ref<EventTarget>` | `window` |
| capture | Use capture mode | `boolean` | `false` |
| passive | Mark listener as passive | `boolean` | `false` |

### Return Value

| Name | Description | Type |
| --- | --- | --- |
| cleanup | Function to manually remove the listener | `() => void` |

## Usage Examples

### Window Resize Event

```vue
<template>
  <div>
    <p>Window width: {{ width }}</p>
    <p>Window height: {{ height }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useEventListener } from '@vant/use';

const width = ref(window.innerWidth);
const height = ref(window.innerHeight);

useEventListener('resize', () => {
  width.value = window.innerWidth;
  height.value = window.innerHeight;
});
</script>
```

### Document Click Event

```vue
<template>
  <div>
    <p>Click count: {{ clickCount }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useEventListener } from '@vant/use';

const clickCount = ref(0);

useEventListener(
  'click',
  () => {
    clickCount.value++;
  },
  { target: document }
);
</script>
```

### Keyboard Events

```vue
<template>
  <div>
    <p>Press any key to see the key code</p>
    <p v-if="lastKey">Last key: {{ lastKey }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useEventListener } from '@vant/use';

const lastKey = ref('');

useEventListener('keydown', (event) => {
  lastKey.value = event.key;
});
</script>
```

### Scroll Event

```vue
<template>
  <div class="scroll-container" ref="container">
    <div class="content">
      <p>Scroll position: {{ scrollTop }}</p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useEventListener } from '@vant/use';

const container = ref();
const scrollTop = ref(0);

useEventListener(
  'scroll',
  () => {
    if (container.value) {
      scrollTop.value = container.value.scrollTop;
    }
  },
  { target: container }
);
</script>

<style scoped>
.scroll-container {
  height: 300px;
  overflow-y: auto;
}

.content {
  height: 1000px;
}
</style>
```

### Manual Cleanup

```vue
<template>
  <div>
    <p>Mouse position: {{ x }}, {{ y }}</p>
    <button @click="toggleTracking">
      {{ isTracking ? 'Stop' : 'Start' }} Tracking
    </button>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useEventListener } from '@vant/use';

const x = ref(0);
const y = ref(0);
const isTracking = ref(false);
let cleanup = null;

const startTracking = () => {
  cleanup = useEventListener('mousemove', (event) => {
    x.value = event.clientX;
    y.value = event.clientY;
  });
  isTracking.value = true;
};

const stopTracking = () => {
  if (cleanup) {
    cleanup();
    cleanup = null;
  }
  isTracking.value = false;
};

const toggleTracking = () => {
  if (isTracking.value) {
    stopTracking();
  } else {
    startTracking();
  }
};
</script>
```

### Passive Event Listener

```vue
<template>
  <div class="touch-area" ref="touchArea">
    <p>Touch events: {{ touchCount }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useEventListener } from '@vant/use';

const touchArea = ref();
const touchCount = ref(0);

useEventListener(
  'touchstart',
  () => {
    touchCount.value++;
  },
  { 
    target: touchArea,
    passive: true 
  }
);
</script>

<style scoped>
.touch-area {
  height: 200px;
  background: #f5f5f5;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
```

### Multiple Events

```vue
<template>
  <div>
    <p>Mouse entered: {{ entered }}</p>
    <p>Clicks inside: {{ clicks }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useEventListener } from '@vant/use';

const entered = ref(false);
const clicks = ref(0);

useEventListener('mouseenter', () => {
  entered.value = true;
});

useEventListener('mouseleave', () => {
  entered.value = false;
});

useEventListener('click', () => {
  clicks.value++;
});
</script>
```

## Best Practices

1. **Default Target**: If no target specified, defaults to window
2. **Passive Events**: Use `passive: true` for scroll/touch events for better performance
3. **Cleanup**: Use the returned cleanup function for conditional event handling
4. **Keep-Alive**: Works correctly with keep-alive components (activate/deactivate)
5. **Multiple Events**: Call useEventListener multiple times for different events
