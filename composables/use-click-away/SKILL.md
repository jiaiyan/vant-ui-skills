---
name: "use-click-away"
description: "Composable for detecting clicks outside of target elements. Invoke when implementing dropdowns, modals, popups, or any UI that needs to close when clicking outside."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# useClickAway

A Vue 3 composable that triggers a callback when the user clicks outside of the target element(s). Perfect for implementing dismissible UI components.

## When to Invoke

Invoke this skill when:
- User needs to close a dropdown menu when clicking outside
- User wants to dismiss a modal or popup on outside click
- User needs to implement click-outside detection for any component
- User wants to handle touch events outside of an element
- User needs to detect clicks outside of multiple elements

## Features

- **Single or Multiple Elements**: Support for single or multiple target elements
- **Custom Events**: Configurable event type (click, touchstart, etc.)
- **Reactive Targets**: Accepts both direct element references and Vue refs
- **Automatic Cleanup**: Event listeners are automatically removed on component unmount
- **TypeScript Support**: Full TypeScript type definitions

## API Reference

### Type Declarations

```ts
type Options = {
  eventName?: string;
};

function useClickAway(
  target:
    | Element
    | Ref<Element | undefined>
    | Array<Element | Ref<Element | undefined>>,
  listener: EventListener,
  options?: Options,
): void;
```

### Parameters

| Name | Description | Type | Default Value |
| --- | --- | --- | --- |
| target | Target element(s) to detect clicks outside of | `Element \| Ref<Element> \| Array<Element \| Ref<Element>>` | - |
| listener | Callback function triggered when clicking outside | `EventListener` | - |
| options | Configuration options | `Options` | `{ eventName: 'click' }` |

### Options

| Name | Description | Type | Default Value |
| --- | --- | --- | --- |
| eventName | The event type to listen for | `string` | `'click'` |

## Usage Examples

### Basic Usage

```vue
<template>
  <div ref="root" class="dropdown">
    <p>Click outside this element to trigger the callback</p>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useClickAway } from '@vant/use';

const root = ref();

useClickAway(root, () => {
  console.log('Clicked outside!');
});
</script>
```

### Dropdown Menu

```vue
<template>
  <div class="dropdown-container">
    <button @click="isOpen = !isOpen">Toggle Dropdown</button>
    <div v-if="isOpen" ref="dropdown" class="dropdown-menu">
      <p>Dropdown content</p>
      <p>Click outside to close</p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useClickAway } from '@vant/use';

const isOpen = ref(false);
const dropdown = ref();

useClickAway(dropdown, () => {
  isOpen.value = false;
});
</script>
```

### Custom Event (Touch)

```vue
<template>
  <div ref="root" class="touch-area">
    <p>Touch outside to trigger</p>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useClickAway } from '@vant/use';

const root = ref();

useClickAway(
  root,
  () => {
    console.log('Touched outside!');
  },
  { eventName: 'touchstart' }
);
</script>
```

### Multiple Elements

```vue
<template>
  <div class="container">
    <div ref="element1" class="box">Element 1</div>
    <div ref="element2" class="box">Element 2</div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useClickAway } from '@vant/use';

const element1 = ref();
const element2 = ref();

useClickAway([element1, element2], () => {
  console.log('Clicked outside both elements!');
});
</script>
```

### Modal with Click Outside to Close

```vue
<template>
  <div>
    <button @click="showModal = true">Open Modal</button>
    
    <Teleport to="body">
      <div v-if="showModal" class="modal-overlay">
        <div ref="modalContent" class="modal-content">
          <h2>Modal Title</h2>
          <p>Click outside to close this modal</p>
        </div>
      </div>
    </Teleport>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';
import { useClickAway } from '@vant/use';

const showModal = ref(false);
const modalContent = ref();

watch(showModal, (visible) => {
  if (visible) {
    useClickAway(modalContent, () => {
      showModal.value = false;
    });
  }
});
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal-content {
  background: white;
  padding: 20px;
  border-radius: 8px;
}
</style>
```

## Best Practices

1. **Use with Dropdowns**: Ideal for closing dropdown menus when clicking outside
2. **Touch Events**: Use `touchstart` for mobile-friendly interactions
3. **Multiple Elements**: Pass an array when you need to exclude multiple areas
4. **Cleanup**: The composable handles cleanup automatically on unmount
5. **Event Choice**: Consider using `mousedown` instead of `click` for faster response
