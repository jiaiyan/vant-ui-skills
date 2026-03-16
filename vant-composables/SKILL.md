---
name: "vant-composables"
description: "Provides an overview of all Vant composables (Vue 3 composition API utilities). Invoke when user needs to explore available composables or find the right composable for their use case."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Composables Overview

This skill provides a comprehensive overview of all Vant composables (Vue 3 composition API utilities), helping developers find the right composable for their needs.

## When to Invoke

Invoke this skill when:
- User wants to explore available Vant composables
- User needs to find a composable for a specific use case
- User asks about composable categories
- User wants a quick reference of all composables
- User needs to implement common Vue 3 patterns

## Composables Index

### State Management

| Composable | Description | Key Features |
|------------|-------------|--------------|
| [useToggle](../composables/use-toggle/SKILL.md) | Toggle boolean state | Simple API, default value support, explicit toggle |
| [useCountDown](../composables/use-count-down/SKILL.md) | Countdown timer logic | Granular time display, control methods, event callbacks |

### Event Handling

| Composable | Description | Key Features |
|------------|-------------|--------------|
| [useClickAway](../composables/use-click-away/SKILL.md) | Detect clicks outside element | Single/multiple elements, custom events, auto cleanup |
| [useEventListener](../composables/use-event-listener/SKILL.md) | Event listener with auto cleanup | Flexible target, manual cleanup, passive support |

### DOM & Layout

| Composable | Description | Key Features |
|------------|-------------|--------------|
| [useRect](../composables/use-rect/SKILL.md) | Element dimensions and position | Full dimensions, viewport relative, window support |
| [useWindowSize](../composables/use-window-size/SKILL.md) | Window dimensions tracking | Reactive, debounced, responsive breakpoints |
| [useScrollParent](../composables/use-scroll-parent/SKILL.md) | Find scrollable parent | Auto detection, window fallback, reactive |

### Lifecycle & Performance

| Composable | Description | Key Features |
|------------|-------------|--------------|
| [useRaf](../composables/use-raf/SKILL.md) | requestAnimationFrame wrapper | Single/loop execution, interval control, cancellation |
| [usePageVisibility](../composables/use-page-visibility/SKILL.md) | Page visibility detection | Real-time tracking, performance optimization |

### Component Relations

| Composable | Description | Key Features |
|------------|-------------|--------------|
| [useRelation](../composables/use-relation/SKILL.md) | Parent-child relationships | Bidirectional communication, index tracking, auto registration |
| [useCustomFieldValue](../composables/use-custom-field-value/SKILL.md) | Custom form field values | Form integration, validation support, reactive values |

## Quick Selection Guide

### For State Management

- **Toggle on/off**: **useToggle** - Simple boolean state switching
- **Countdown timer**: **useCountDown** - Time-based countdown with controls

### For Event Handling

- **Close on outside click**: **useClickAway** - Dropdowns, modals, popups
- **Window/document events**: **useEventListener** - Resize, scroll, keyboard

### For Layout & Positioning

- **Element dimensions**: **useRect** - Size and position relative to viewport
- **Responsive design**: **useWindowSize** - Window width/height tracking
- **Scroll containers**: **useScrollParent** - Find scrollable parent element

### For Animations

- **Smooth animations**: **useRaf** - requestAnimationFrame wrapper
- **Pause when hidden**: **usePageVisibility** - Detect tab visibility

### For Component Communication

- **Parent-child link**: **useRelation** - Compound component patterns
- **Custom form inputs**: **useCustomFieldValue** - Integrate with van-form

## API Summary

### useToggle

```ts
function useToggle(defaultValue?: boolean): [Ref<boolean>, (newValue?: boolean) => void]
```

**Parameters**: `defaultValue` (boolean, default: `false`)

**Returns**: `[state, toggle]` - state ref and toggle function

### useCountDown

```ts
function useCountDown(options: {
  time: number;
  millisecond?: boolean;
  onChange?: (current: CurrentTime) => void;
  onFinish?: () => void;
}): { start, pause, reset, current }
```

**Returns**: Control methods and current time object

### useClickAway

```ts
function useClickAway(
  target: Element | Ref<Element> | Array<Element | Ref<Element>>,
  listener: EventListener,
  options?: { eventName?: string }
): void
```

### useEventListener

```ts
function useEventListener(
  type: string,
  listener: EventListener,
  options?: { target?: EventTarget | Ref<EventTarget>; capture?: boolean; passive?: boolean }
): () => void
```

**Returns**: Cleanup function

### useRect

```ts
function useRect(element: Element | Window | Ref<Element | Window | undefined>): DOMRect
```

**Returns**: `{ width, height, top, left, right, bottom }`

### useWindowSize

```ts
function useWindowSize(): { width: Ref<number>; height: Ref<number> }
```

### useScrollParent

```ts
function useScrollParent(element: Ref<Element | undefined>): Ref<Element | Window | undefined>
```

### useRaf

```ts
function useRaf(
  callback: () => void,
  options?: { interval?: number; isLoop?: boolean }
): () => void
```

**Returns**: Cancel function

### usePageVisibility

```ts
function usePageVisibility(): Ref<'visible' | 'hidden'>
```

### useRelation

```ts
function useParent<T>(key: string | symbol): { parent?: T; index?: Ref<number> }
function useChildren(key: string | symbol): { children: ComponentPublicInstance[]; linkChildren: (value: any) => void }
```

### useCustomFieldValue

```ts
function useCustomFieldValue(customValue: () => unknown): void
```

## Common Usage Patterns

### Modal with Click Outside Close

```vue
<template>
  <div v-if="visible" class="modal-overlay">
    <div ref="modalContent" class="modal-content">
      Modal content
    </div>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';
import { useClickAway } from '@vant/use';

const visible = ref(false);
const modalContent = ref();

watch(visible, (isVisible) => {
  if (isVisible) {
    useClickAway(modalContent, () => {
      visible.value = false;
    });
  }
});
</script>
```

### Responsive Breakpoints

```vue
<template>
  <div :class="deviceClass">
    Current device: {{ deviceType }}
  </div>
</template>

<script setup>
import { computed } from 'vue';
import { useWindowSize } from '@vant/use';

const { width } = useWindowSize();

const deviceType = computed(() => {
  if (width.value < 576) return 'mobile';
  if (width.value < 768) return 'tablet';
  if (width.value < 992) return 'laptop';
  return 'desktop';
});
</script>
```

### Countdown Timer

```vue
<template>
  <div>
    <p>{{ current.minutes }}:{{ String(current.seconds).padStart(2, '0') }}</p>
    <button @click="start">Start</button>
    <button @click="pause">Pause</button>
    <button @click="reset()">Reset</button>
  </div>
</template>

<script setup>
import { useCountDown } from '@vant/use';

const { current, start, pause, reset } = useCountDown({
  time: 5 * 60 * 1000,
  onFinish: () => console.log('Done!'),
});
</script>
```

### Animation Loop

```vue
<template>
  <div class="box" :style="{ transform: `translateX(${position}px)` }" />
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import { useRaf } from '@vant/use';

const position = ref(0);
let cancel = null;

onMounted(() => {
  cancel = useRaf(
    () => { position.value = (position.value + 2) % 300; },
    { isLoop: true }
  );
});

onUnmounted(() => cancel?.());
</script>
```

## Best Practices

1. **Import from @vant/use**: All composables are exported from `@vant/use` package

2. **Auto Cleanup**: Most composables handle cleanup automatically on component unmount

3. **Reactive Targets**: Accept refs for dynamic element references

4. **TypeScript**: Full TypeScript support with type definitions

5. **Combine Composables**: Composables can be combined for complex patterns

## Input Parameters

When using this skill, provide the following information:
- **Use case**: What functionality is needed
- **Category**: Which composable category to focus on
- **Features**: Specific features required

## Output Format

This skill provides:
1. Composable category overview
2. Composable recommendations based on use case
3. API summary with parameters and return values
4. Common usage patterns
5. Links to detailed composable documentation

## Usage Limitations

- This is an overview skill; for detailed composable usage, refer to specific composable documentation
- Composable availability may vary by Vant version
- Some composables require additional setup
