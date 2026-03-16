---
name: "use-scroll-parent"
description: "Composable for finding the nearest scrollable parent element. Invoke when implementing scroll-based features like lazy loading, sticky headers, or scroll listeners."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# useScrollParent

A Vue 3 composable that finds the closest parent element that is scrollable, useful for attaching scroll event listeners.

## When to Invoke

Invoke this skill when:
- User needs to find the scrollable container of an element
- User wants to attach scroll event listeners to the correct parent
- User needs to implement infinite scroll or lazy loading
- User wants to create sticky elements within scroll containers
- User needs to detect scroll position relative to a container

## Features

- **Auto Detection**: Automatically finds the nearest scrollable parent
- **Reactive**: Returns a ref that updates if parent changes
- **Window Fallback**: Returns window if no scrollable parent found
- **Performance**: Efficient DOM traversal
- **TypeScript Support**: Full TypeScript type definitions

## API Reference

### Type Declarations

```ts
function useScrollParent(
  element: Ref<Element | undefined>,
): Ref<Element | Window | undefined>;
```

### Parameters

| Name | Description | Type |
| --- | --- | --- |
| element | The target element ref | `Ref<Element \| undefined>` |

### Return Value

| Name | Description | Type |
| --- | --- | --- |
| scrollParent | The nearest scrollable parent element | `Ref<Element \| Window \| undefined>` |

## Usage Examples

### Basic Usage

```vue
<template>
  <div ref="root" class="element">
    <p>Scroll parent detected</p>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';
import { useScrollParent } from '@vant/use';

const root = ref();
const scrollParent = useScrollParent(root);

watch(scrollParent, (parent) => {
  console.log('Scroll parent:', parent);
});
</script>
```

### Scroll Event Listener

```vue
<template>
  <div class="scroll-container">
    <div ref="target" class="content">
      <p>Scroll position: {{ scrollPosition }}</p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useScrollParent, useEventListener } from '@vant/use';

const target = ref();
const scrollPosition = ref(0);

const scrollParent = useScrollParent(target);

useEventListener(
  'scroll',
  () => {
    if (scrollParent.value === window) {
      scrollPosition.value = window.scrollY;
    } else if (scrollParent.value) {
      scrollPosition.value = scrollParent.value.scrollTop;
    }
  },
  { target: scrollParent }
);
</script>

<style scoped>
.scroll-container {
  height: 300px;
  overflow-y: auto;
  border: 1px solid #ddd;
}

.content {
  height: 1000px;
  padding: 20px;
}
</style>
```

### Lazy Loading Images

```vue
<template>
  <div class="scroll-container">
    <div v-for="item in items" :key="item.id" class="item">
      <img 
        ref="images"
        :src="isVisible(item.id) ? item.url : placeholder"
        :alt="item.title"
      />
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useScrollParent, useEventListener, useRect } from '@vant/use';

const images = ref([]);
const visibleItems = ref(new Set());
const scrollParent = ref();

const items = [
  { id: 1, url: 'image1.jpg', title: 'Image 1' },
  { id: 2, url: 'image2.jpg', title: 'Image 2' },
  // ... more items
];

const placeholder = 'placeholder.jpg';

const checkVisibility = () => {
  images.value.forEach((img, index) => {
    if (!img) return;
    
    const rect = useRect(img);
    const viewportHeight = window.innerHeight;
    
    if (rect.top < viewportHeight && rect.bottom > 0) {
      visibleItems.value.add(items[index].id);
    }
  });
};

onMounted(() => {
  if (images.value[0]) {
    scrollParent.value = useScrollParent(ref(images.value[0]));
    useEventListener('scroll', checkVisibility, { target: scrollParent });
    checkVisibility();
  }
});

const isVisible = (id) => visibleItems.value.has(id);
</script>
```

### Sticky Header in Scroll Container

```vue
<template>
  <div class="page">
    <div class="scroll-container">
      <div ref="content" class="content">
        <div class="header" :class="{ sticky: isSticky }">
          Sticky Header
        </div>
        <div class="body">
          <p v-for="i in 50" :key="i">Content line {{ i }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useScrollParent, useEventListener, useRect } from '@vant/use';

const content = ref();
const isSticky = ref(false);

const scrollParent = useScrollParent(content);

useEventListener(
  'scroll',
  () => {
    if (!content.value) return;
    
    const rect = useRect(content);
    isSticky.value = rect.top < 0;
  },
  { target: scrollParent }
);
</script>

<style scoped>
.scroll-container {
  height: 400px;
  overflow-y: auto;
  border: 1px solid #ddd;
}

.header {
  background: #409eff;
  color: white;
  padding: 16px;
  transition: all 0.3s;
}

.header.sticky {
  position: sticky;
  top: 0;
  z-index: 10;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15);
}

.body {
  padding: 16px;
}
</style>
```

### Infinite Scroll

```vue
<template>
  <div class="scroll-container">
    <div ref="list" class="list">
      <div v-for="item in items" :key="item" class="item">
        Item {{ item }}
      </div>
      <div v-if="loading" class="loading">Loading...</div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useScrollParent, useEventListener, useRect } from '@vant/use';

const list = ref();
const items = ref(Array.from({ length: 20 }, (_, i) => i + 1));
const loading = ref(false);
const page = ref(1);

const scrollParent = useScrollParent(list);

const loadMore = async () => {
  if (loading.value) return;
  
  loading.value = true;
  
  await new Promise(resolve => setTimeout(resolve, 1000));
  
  const newItems = Array.from(
    { length: 10 },
    (_, i) => items.value.length + i + 1
  );
  items.value.push(...newItems);
  page.value++;
  loading.value = false;
};

const checkScroll = () => {
  if (!list.value || !scrollParent.value) return;
  
  const listRect = useRect(list.value);
  const parentHeight = scrollParent.value === window
    ? window.innerHeight
    : (scrollParent.value as Element).clientHeight;
  
  if (listRect.bottom - parentHeight < 100) {
    loadMore();
  }
};

useEventListener('scroll', checkScroll, { target: scrollParent });
</script>

<style scoped>
.scroll-container {
  height: 400px;
  overflow-y: auto;
  border: 1px solid #ddd;
}

.item {
  padding: 16px;
  border-bottom: 1px solid #eee;
}

.loading {
  padding: 16px;
  text-align: center;
  color: #999;
}
</style>
```

### Scroll to Element

```vue
<template>
  <div class="scroll-container" ref="container">
    <div v-for="i in 20" :key="i" :ref="el => setItemRef(el, i)" class="item">
      Item {{ i }}
    </div>
  </div>
  <button @click="scrollToItem(10)">Scroll to Item 10</button>
</template>

<script setup>
import { ref } from 'vue';
import { useScrollParent } from '@vant/use';

const container = ref();
const itemRefs = ref({});

const scrollParent = useScrollParent(container);

const setItemRef = (el, index) => {
  if (el) {
    itemRefs.value[index] = el;
  }
};

const scrollToItem = (index) => {
  const element = itemRefs.value[index];
  if (element && scrollParent.value) {
    element.scrollIntoView({ behavior: 'smooth', block: 'center' });
  }
};
</script>

<style scoped>
.scroll-container {
  height: 300px;
  overflow-y: auto;
  border: 1px solid #ddd;
}

.item {
  padding: 20px;
  border-bottom: 1px solid #eee;
}
</style>
```

## Best Practices

1. **Check for Window**: The returned parent might be window
2. **Use with useEventListener**: Combine with useEventListener for scroll handling
3. **Reactive Updates**: The scroll parent ref updates automatically
4. **Performance**: Cache scroll parent for repeated operations
5. **Nested Containers**: Finds the nearest scrollable ancestor
