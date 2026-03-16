---
name: "use-relation"
description: "Composable for establishing parent-child component relationships. Invoke when implementing compound components that need communication between parent and children."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# useRelation

A Vue 3 composable for establishing relationships between parent and child components, enabling data communication and method invocation based on Vue's `provide` and `inject`.

## When to Invoke

Invoke this skill when:
- User needs to create compound components (Tabs, Form, etc.)
- User wants parent-child communication without prop drilling
- User needs to track child component indices
- User wants to share state between parent and children
- User needs to implement component registries

## Features

- **Parent-Child Link**: Establish bidirectional communication
- **Index Tracking**: Children know their position in parent
- **Data Sharing**: Share any data or methods between components
- **Reactive**: Works with Vue's reactivity system
- **Automatic Registration**: Children auto-register with parent
- **TypeScript Support**: Full TypeScript type definitions

## API Reference

### Type Declarations

```ts
function useParent<T>(key: string | symbol): {
  parent?: T;
  index?: Ref<number>;
};

function useChildren(key: string | symbol): {
  children: ComponentPublicInstance[];
  linkChildren: (value: any) => void;
};
```

### useParent Return Value

| Name | Description | Type |
| --- | --- | --- |
| parent | Data and methods provided by parent | `T \| undefined` |
| index | Index position in parent's children array | `Ref<number> \| undefined` |

### useChildren Return Value

| Name | Description | Type |
| --- | --- | --- |
| children | Array of child component instances | `ComponentPublicInstance[]` |
| linkChildren | Function to provide values to children | `(value: any) => void` |

## Usage Examples

### Basic Parent-Child Relationship

```vue
<template>
  <div class="parent">
    <p>Count from parent: {{ count }}</p>
    <slot />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useChildren } from '@vant/use';

const RELATION_KEY = Symbol('parent-child');

const { linkChildren } = useChildren(RELATION_KEY);

const count = ref(0);
const increment = () => {
  count.value++;
};

linkChildren({ count, increment });
</script>
```

```vue
<template>
  <div class="child">
    <p>Child index: {{ index }}</p>
    <button @click="parent?.increment">
      Increment Parent Count
    </button>
  </div>
</template>

<script setup>
import { useParent } from '@vant/use';

const RELATION_KEY = Symbol('parent-child');

const { parent, index } = useParent(RELATION_KEY);
</script>
```

### Tabs Component

```vue
<template>
  <div class="tabs">
    <div class="tab-list">
      <slot name="tabs" />
    </div>
    <div class="tab-content">
      <slot />
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import { useChildren } from '@vant/use';

const TABS_KEY = Symbol('tabs');

const { children, linkChildren } = useChildren(TABS_KEY);

const activeIndex = ref(0);

const setActive = (index) => {
  activeIndex.value = index;
};

linkChildren({
  activeIndex,
  setActive,
});
</script>
```

```vue
<template>
  <div 
    class="tab" 
    :class="{ active: isActive }"
    @click="select"
  >
    <slot />
  </div>
</template>

<script setup>
import { computed } from 'vue';
import { useParent } from '@vant/use';

const TABS_KEY = Symbol('tabs');

const props = defineProps({
  title: String,
});

const { parent, index } = useParent(TABS_KEY);

const isActive = computed(() => {
  return parent && index.value === parent.activeIndex.value;
});

const select = () => {
  parent?.setActive(index.value);
};
</script>
```

### Radio Group

```vue
<template>
  <div class="radio-group">
    <slot />
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';
import { useChildren } from '@vant/use';

const RADIO_GROUP_KEY = Symbol('radio-group');

const props = defineProps({
  modelValue: [String, Number],
});

const emit = defineEmits(['update:modelValue']);

const { children, linkChildren } = useChildren(RADIO_GROUP_KEY);

const updateValue = (value) => {
  emit('update:modelValue', value);
};

linkChildren({
  modelValue: computed(() => props.modelValue),
  updateValue,
});
</script>
```

```vue
<template>
  <label class="radio" :class="{ checked: isChecked }">
    <input 
      type="radio" 
      :checked="isChecked"
      @change="onChange"
    />
    <slot />
  </label>
</template>

<script setup>
import { computed } from 'vue';
import { useParent } from '@vant/use';

const RADIO_GROUP_KEY = Symbol('radio-group');

const props = defineProps({
  value: [String, Number],
});

const { parent } = useParent(RADIO_GROUP_KEY);

const isChecked = computed(() => {
  return parent && parent.modelValue.value === props.value;
});

const onChange = () => {
  parent?.updateValue(props.value);
};
</script>
```

### Form Field Registry

```vue
<template>
  <form @submit.prevent="handleSubmit">
    <slot />
    <button type="submit">Submit</button>
  </form>
</template>

<script setup>
import { ref } from 'vue';
import { useChildren } from '@vant/use';

const FORM_KEY = Symbol('form');

const { children, linkChildren } = useChildren(FORM_KEY);

const registerField = (field) => {
  // Children are automatically tracked
};

const validateAll = async () => {
  const results = await Promise.all(
    children.map(child => child.validate?.())
  );
  return results.every(Boolean);
};

const handleSubmit = async () => {
  const isValid = await validateAll();
  if (isValid) {
    console.log('Form is valid');
  }
};

linkChildren({
  registerField,
  validateAll,
});
</script>
```

### Accordion Component

```vue
<template>
  <div class="accordion">
    <slot />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useChildren } from '@vant/use';

const ACCORDION_KEY = Symbol('accordion');

const props = defineProps({
  modelValue: [Number, Array],
});

const emit = defineEmits(['update:modelValue']);

const { children, linkChildren } = useChildren(ACCORDION_KEY);

const toggle = (index) => {
  if (props.modelValue === index) {
    emit('update:modelValue', -1);
  } else {
    emit('update:modelValue', index);
  }
};

linkChildren({
  activeIndex: computed(() => props.modelValue),
  toggle,
});
</script>
```

```vue
<template>
  <div class="accordion-item">
    <div class="header" @click="toggle">
      <slot name="header" />
      <span>{{ isOpen ? '−' : '+' }}</span>
    </div>
    <div v-show="isOpen" class="content">
      <slot />
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue';
import { useParent } from '@vant/use';

const ACCORDION_KEY = Symbol('accordion');

const { parent, index } = useParent(ACCORDION_KEY);

const isOpen = computed(() => {
  return parent && parent.activeIndex.value === index.value;
});

const toggle = () => {
  parent?.toggle(index.value);
};
</script>
```

## Best Practices

1. **Unique Keys**: Use Symbol for relation keys to avoid conflicts
2. **Optional Parent**: Always check if parent exists before using
3. **Reactive Data**: Use computed or ref for shared reactive data
4. **Cleanup**: Children are automatically removed when unmounted
5. **Type Safety**: Define types for shared data structure
