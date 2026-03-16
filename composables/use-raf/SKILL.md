---
name: "use-raf"
description: "Composable for requestAnimationFrame with convenient call and cancellation. Invoke when implementing animations, game loops, or any visual updates synchronized with browser repaints."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# useRaf

A Vue 3 composable that provides convenient call and cancellation of `requestAnimationFrame`, perfect for smooth animations and visual updates.

## When to Invoke

Invoke this skill when:
- User needs to implement smooth animations
- User wants to create game loops or continuous visual updates
- User needs to synchronize updates with browser repaints
- User wants to execute code before next repaint
- User needs interval-based animations with RAF

## Features

- **Single Execution**: Execute once before next repaint
- **Loop Mode**: Continuous execution at specified intervals
- **Interval Control**: Set custom interval for loop mode
- **Cancellation**: Easy cancellation of scheduled callbacks
- **Performance**: Uses native requestAnimationFrame
- **TypeScript Support**: Full TypeScript type definitions

## API Reference

### Type Declarations

```ts
function useRaf(
  callback: () => void,
  options?: {
    interval?: number;
    isLoop?: boolean;
  },
): () => void;
```

### Parameters

| Name | Description | Type | Default |
| --- | --- | --- | --- |
| callback | Function to execute | `() => void` | - |
| options | Configuration options | `{ interval?: number; isLoop?: boolean }` | `{ interval: 0, isLoop: false }` |

### Options

| Name | Description | Type | Default |
| --- | --- | --- | --- |
| interval | Time between calls in milliseconds (loop mode) | `number` | `0` |
| isLoop | Enable continuous execution | `boolean` | `false` |

### Return Value

| Name | Description | Type |
| --- | --- | --- |
| cancel | Function to cancel the RAF | `() => void` |

## Usage Examples

### Single Execution

```vue
<template>
  <div>
    <p>Count: {{ count }}</p>
    <button @click="executeOnce">Execute Once</button>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRaf } from '@vant/use';

const count = ref(0);

const executeOnce = () => {
  useRaf(() => {
    count.value++;
    console.log('Executed once');
  });
};
</script>
```

### Animation Loop

```vue
<template>
  <div>
    <div class="box" :style="{ transform: `translateX(${position}px)` }" />
    <button @click="toggleAnimation">
      {{ isAnimating ? 'Stop' : 'Start' }} Animation
    </button>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRaf } from '@vant/use';

const position = ref(0);
const isAnimating = ref(false);
let cancelAnimation = null;

const animate = () => {
  position.value = (position.value + 2) % 300;
  
  if (isAnimating.value) {
    cancelAnimation = useRaf(animate);
  }
};

const toggleAnimation = () => {
  isAnimating.value = !isAnimating.value;
  
  if (isAnimating.value) {
    animate();
  } else if (cancelAnimation) {
    cancelAnimation();
  }
};
</script>

<style scoped>
.box {
  width: 50px;
  height: 50px;
  background: #409eff;
  border-radius: 4px;
}
</style>
```

### Loop with Interval

```vue
<template>
  <div>
    <p>Counter: {{ count }}</p>
    <button @click="startLoop">Start Loop</button>
    <button @click="stopLoop">Stop Loop</button>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRaf } from '@vant/use';

const count = ref(0);
let cancelLoop = null;

const startLoop = () => {
  count.value = 0;
  
  cancelLoop = useRaf(
    () => {
      count.value++;
      console.log('Loop iteration:', count.value);
      
      if (count.value >= 10) {
        stopLoop();
      }
    },
    {
      isLoop: true,
      interval: 100,
    }
  );
};

const stopLoop = () => {
  if (cancelLoop) {
    cancelLoop();
    cancelLoop = null;
  }
};
</script>
```

### Smooth Counter

```vue
<template>
  <div>
    <p>Target: {{ target }}</p>
    <p>Current: {{ current.toFixed(0) }}</p>
    <button @click="animateTo(target + 100)">Add 100</button>
    <button @click="animateTo(target - 100)">Subtract 100</button>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRaf } from '@vant/use';

const target = ref(0);
const current = ref(0);
let cancelAnimation = null;

const animateTo = (newTarget) => {
  target.value = newTarget;
  
  if (cancelAnimation) {
    cancelAnimation();
  }
  
  cancelAnimation = useRaf(
    () => {
      const diff = target.value - current.value;
      
      if (Math.abs(diff) < 1) {
        current.value = target.value;
        cancelAnimation?.();
        return;
      }
      
      current.value += diff * 0.1;
    },
    { isLoop: true }
  );
};
</script>
```

### Canvas Animation

```vue
<template>
  <canvas ref="canvas" width="400" height="300" />
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import { useRaf } from '@vant/use';

const canvas = ref();
let cancelAnimation = null;

onMounted(() => {
  const ctx = canvas.value.getContext('2d');
  let x = 0;
  let y = 150;
  let dx = 2;
  let dy = 2;
  
  const draw = () => {
    ctx.clearRect(0, 0, 400, 300);
    
    ctx.beginPath();
    ctx.arc(x, y, 20, 0, Math.PI * 2);
    ctx.fillStyle = '#409eff';
    ctx.fill();
    
    x += dx;
    y += dy;
    
    if (x <= 20 || x >= 380) dx = -dx;
    if (y <= 20 || y >= 280) dy = -dy;
  };
  
  cancelAnimation = useRaf(draw, { isLoop: true });
});

onUnmounted(() => {
  cancelAnimation?.();
});
</script>
```

### Progress Bar Animation

```vue
<template>
  <div>
    <div class="progress-bar">
      <div class="progress" :style="{ width: progress + '%' }" />
    </div>
    <button @click="startProgress">Start Progress</button>
    <button @click="resetProgress">Reset</button>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRaf } from '@vant/use';

const progress = ref(0);
let cancelAnimation = null;

const startProgress = () => {
  if (cancelAnimation) {
    cancelAnimation();
  }
  
  cancelAnimation = useRaf(
    () => {
      if (progress.value < 100) {
        progress.value += 0.5;
      } else {
        cancelAnimation?.();
      }
    },
    { isLoop: true, interval: 16 }
  );
};

const resetProgress = () => {
  cancelAnimation?.();
  progress.value = 0;
};
</script>

<style scoped>
.progress-bar {
  width: 100%;
  height: 20px;
  background: #f5f5f5;
  border-radius: 10px;
  overflow: hidden;
  margin-bottom: 16px;
}

.progress {
  height: 100%;
  background: linear-gradient(90deg, #409eff, #67c23a);
  transition: width 0.1s linear;
}
</style>
```

### FPS Counter

```vue
<template>
  <div class="fps-counter">
    <p>FPS: {{ fps }}</p>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import { useRaf } from '@vant/use';

const fps = ref(0);
let cancelAnimation = null;

onMounted(() => {
  let lastTime = performance.now();
  let frameCount = 0;
  
  const updateFPS = () => {
    frameCount++;
    const currentTime = performance.now();
    
    if (currentTime - lastTime >= 1000) {
      fps.value = frameCount;
      frameCount = 0;
      lastTime = currentTime;
    }
  };
  
  cancelAnimation = useRaf(updateFPS, { isLoop: true });
});

onUnmounted(() => {
  cancelAnimation?.();
});
</script>

<style scoped>
.fps-counter {
  position: fixed;
  top: 10px;
  right: 10px;
  background: rgba(0, 0, 0, 0.7);
  color: white;
  padding: 8px 12px;
  border-radius: 4px;
  font-family: monospace;
}
</style>
```

### Scroll Animation

```vue
<template>
  <div>
    <div class="content">
      <p v-for="i in 50" :key="i">Line {{ i }}</p>
    </div>
    <button @click="scrollToTop">Scroll to Top</button>
  </div>
</template>

<script setup>
import { useRaf } from '@vant/use';

const scrollToTop = () => {
  const startPosition = window.scrollY;
  const duration = 500;
  const startTime = performance.now();
  
  const animate = () => {
    const elapsed = performance.now() - startTime;
    const progress = Math.min(elapsed / duration, 1);
    
    const easeOut = 1 - Math.pow(1 - progress, 3);
    
    window.scrollTo(0, startPosition * (1 - easeOut));
    
    if (progress < 1) {
      useRaf(animate);
    }
  };
  
  useRaf(animate);
};
</script>

<style scoped>
.content {
  height: 2000px;
  padding: 20px;
}

button {
  position: fixed;
  bottom: 20px;
  right: 20px;
}
</style>
```

## Best Practices

1. **Cancel on Unmount**: Always cancel RAF on component unmount
2. **Loop Mode**: Use `isLoop: true` for continuous animations
3. **Interval**: Set appropriate interval for performance
4. **Cleanup**: Store cancel function and call when done
5. **Performance**: RAF is more efficient than setInterval for animations
