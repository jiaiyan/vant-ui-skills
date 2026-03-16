---
name: "use-rect"
description: "Composable for getting element dimensions and position. Invoke when needing to measure element size, position relative to viewport, or implement positioning logic."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# useRect

A Vue 3 composable that retrieves the size of an element and its position relative to the viewport, equivalent to `Element.getBoundingClientRect()`.

## When to Invoke

Invoke this skill when:
- User needs to get element dimensions (width, height)
- User wants to calculate element position relative to viewport
- User needs to implement tooltip or popover positioning
- User wants to detect element visibility in viewport
- User needs to implement drag and drop positioning

## Features

- **Full Dimensions**: Provides width, height, top, left, right, bottom
- **Viewport Relative**: All values are relative to the viewport
- **Window Support**: Works with both Element and Window
- **Reactive Target**: Accepts Vue refs for dynamic elements
- **Simple API**: Returns a DOMRect-like object
- **TypeScript Support**: Full TypeScript type definitions

## API Reference

### Type Declarations

```ts
function useRect(
  element: Element | Window | Ref<Element | Window | undefined>,
): DOMRect;
```

### Parameters

| Name | Description | Type |
| --- | --- | --- |
| element | Target element or window | `Element \| Window \| Ref<Element \| Window \| undefined>` |

### Return Value

| Name | Description | Type |
| --- | --- | --- |
| width | Width of the element | `number` |
| height | Height of the element | `number` |
| top | Distance from top to viewport top | `number` |
| left | Distance from left to viewport left | `number` |
| right | Distance from right to viewport left | `number` |
| bottom | Distance from bottom to viewport top | `number` |

## Usage Examples

### Basic Usage

```vue
<template>
  <div ref="root" class="box">
    <p>Element dimensions and position</p>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRect } from '@vant/use';

const root = ref();

onMounted(() => {
  const rect = useRect(root);
  console.log('Element rect:', rect);
});
</script>
```

### Display Element Info

```vue
<template>
  <div>
    <div ref="target" class="target-box">
      Resize or scroll to see changes
    </div>
    <div class="info">
      <p>Width: {{ rect?.width.toFixed(0) }}px</p>
      <p>Height: {{ rect?.height.toFixed(0) }}px</p>
      <p>Top: {{ rect?.top.toFixed(0) }}px</p>
      <p>Left: {{ rect?.left.toFixed(0) }}px</p>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUpdated } from 'vue';
import { useRect } from '@vant/use';

const target = ref();
const rect = ref(null);

const updateRect = () => {
  if (target.value) {
    rect.value = useRect(target);
  }
};

onMounted(updateRect);
onUpdated(updateRect);
</script>

<style scoped>
.target-box {
  width: 200px;
  height: 100px;
  background: #409eff;
  color: white;
  padding: 20px;
  margin: 50px;
}

.info {
  position: fixed;
  top: 10px;
  right: 10px;
  background: white;
  padding: 10px;
  border: 1px solid #ddd;
}
</style>
```

### Tooltip Positioning

```vue
<template>
  <div class="container">
    <button 
      ref="trigger" 
      @mouseenter="showTooltip" 
      @mouseleave="hideTooltip"
    >
      Hover me
    </button>
    
    <div 
      v-if="visible" 
      class="tooltip" 
      :style="tooltipStyle"
    >
      Tooltip content
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import { useRect } from '@vant/use';

const trigger = ref();
const visible = ref(false);

const tooltipStyle = computed(() => {
  if (!trigger.value) return {};
  
  const rect = useRect(trigger);
  return {
    position: 'fixed',
    top: `${rect.bottom + 8}px`,
    left: `${rect.left}px`,
  };
});

const showTooltip = () => {
  visible.value = true;
};

const hideTooltip = () => {
  visible.value = false;
};
</script>

<style scoped>
.tooltip {
  background: #333;
  color: white;
  padding: 8px 12px;
  border-radius: 4px;
  font-size: 14px;
  z-index: 1000;
}
</style>
```

### Detect Visibility in Viewport

```vue
<template>
  <div class="scroll-container" @scroll="checkVisibility">
    <div class="spacer" />
    <div ref="target" class="target" :class="{ visible: isVisible }">
      {{ isVisible ? 'Visible' : 'Not visible' }}
    </div>
    <div class="spacer" />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRect } from '@vant/use';

const target = ref();
const isVisible = ref(false);

const checkVisibility = () => {
  if (!target.value) return;
  
  const rect = useRect(target);
  const windowHeight = window.innerHeight;
  
  isVisible.value = (
    rect.top < windowHeight &&
    rect.bottom > 0
  );
};
</script>

<style scoped>
.scroll-container {
  height: 300px;
  overflow-y: auto;
  border: 1px solid #ddd;
}

.spacer {
  height: 400px;
}

.target {
  height: 100px;
  background: #ccc;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background 0.3s;
}

.target.visible {
  background: #67c23a;
  color: white;
}
</style>
```

### Center Element in Viewport

```vue
<template>
  <div>
    <button @click="centerElement">Center Element</button>
    <div ref="element" class="movable">
      Click button to center me
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRect } from '@vant/use';

const element = ref();

const centerElement = () => {
  if (!element.value) return;
  
  const rect = useRect(element);
  const viewportWidth = window.innerWidth;
  const viewportHeight = window.innerHeight;
  
  const scrollTop = window.pageYOffset;
  const scrollLeft = window.pageXOffset;
  
  const targetTop = scrollTop + (viewportHeight - rect.height) / 2;
  const targetLeft = scrollLeft + (viewportWidth - rect.width) / 2;
  
  element.value.style.position = 'absolute';
  element.value.style.top = `${targetTop}px`;
  element.value.style.left = `${targetLeft}px`;
};
</script>

<style scoped>
.movable {
  width: 200px;
  height: 100px;
  background: #409eff;
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 8px;
}
</style>
```

### Compare Two Elements

```vue
<template>
  <div>
    <div ref="elem1" class="box">Element 1</div>
    <div ref="elem2" class="box">Element 2</div>
    <button @click="compareElements">Compare Positions</button>
    <p v-if="comparison">{{ comparison }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRect } from '@vant/use';

const elem1 = ref();
const elem2 = ref();
const comparison = ref('');

const compareElements = () => {
  if (!elem1.value || !elem2.value) return;
  
  const rect1 = useRect(elem1);
  const rect2 = useRect(elem2);
  
  if (rect1.top < rect2.top) {
    comparison.value = 'Element 1 is above Element 2';
  } else {
    comparison.value = 'Element 2 is above Element 1';
  }
};
</script>

<style scoped>
.box {
  width: 100px;
  height: 100px;
  background: #409eff;
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 20px;
}
</style>
```

## Best Practices

1. **Call After Mount**: Ensure element is rendered before calling useRect
2. **Update on Changes**: Re-call when layout changes occur
3. **Performance**: Cache results if called frequently
4. **Scroll Position**: Values are viewport-relative, account for scroll
5. **Transforms**: CSS transforms may affect returned values
