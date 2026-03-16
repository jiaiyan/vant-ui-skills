---
name: "use-custom-field-value"
description: "Composable for customizing Field component values in Vant forms. Invoke when creating custom form inputs that need to integrate with van-form validation and submission."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# useCustomFieldValue

A Vue 3 composable for customizing Field component values, enabling seamless integration with Vant's Form validation and submission system.

## When to Invoke

Invoke this skill when:
- User needs to create a custom form input component
- User wants to integrate custom components with van-form
- User needs to implement non-standard input types (rating, color picker, etc.)
- User wants to use van-field's input slot with custom components
- User needs form validation for custom input components

## Features

- **Form Integration**: Seamlessly integrates with van-form validation
- **Custom Input Types**: Support for any custom input component
- **Reactive Values**: Automatically syncs with form submission
- **Validation Support**: Works with Vant's form validation rules
- **TypeScript Support**: Full TypeScript type definitions

## API Reference

### Type Declarations

```ts
function useCustomFieldValue(customValue: () => unknown): void;
```

### Parameters

| Name | Description | Type | Default Value |
| --- | --- | --- | --- |
| customValue | Function that returns the current field value | `() => unknown` | - |

## Usage Examples

### Basic Custom Input

```vue
<template>
  <div class="custom-input">
    <button @click="decrement">-</button>
    <span>{{ myValue }}</span>
    <button @click="increment">+</button>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useCustomFieldValue } from '@vant/use';

const myValue = ref(0);

const increment = () => myValue.value++;
const decrement = () => myValue.value--;

useCustomFieldValue(() => myValue.value);
</script>
```

### Integration with van-field

```vue
<template>
  <van-form @submit="onSubmit">
    <van-field name="counter" label="Counter">
      <template #input>
        <counter-input v-model="counterValue" />
      </template>
    </van-field>
    
    <van-field name="rating" label="Rating">
      <template #input>
        <rating-input v-model="ratingValue" />
      </template>
    </van-field>
    
    <div style="margin: 16px;">
      <van-button round block type="primary" native-type="submit">
        Submit
      </van-button>
    </div>
  </van-form>
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const counterValue = ref(0);
const ratingValue = ref(3);

const onSubmit = (values) => {
  console.log('Form values:', values);
  showToast('Submitted');
};
</script>
```

### Rating Input Component

```vue
<template>
  <div class="rating-input">
    <van-icon 
      v-for="i in max" 
      :key="i"
      :name="i <= modelValue ? 'star' : 'star-o'"
      :color="i <= modelValue ? '#ffd21e' : '#c8c9cc'"
      size="24"
      @click="selectRating(i)"
    />
  </div>
</template>

<script setup>
import { useCustomFieldValue } from '@vant/use';

const props = defineProps({
  modelValue: {
    type: Number,
    default: 0,
  },
  max: {
    type: Number,
    default: 5,
  },
});

const emit = defineEmits(['update:modelValue']);

const selectRating = (value) => {
  emit('update:modelValue', value);
};

useCustomFieldValue(() => props.modelValue);
</script>

<style scoped>
.rating-input {
  display: flex;
  gap: 4px;
}
</style>
```

### Color Picker Input

```vue
<template>
  <div class="color-picker">
    <div 
      v-for="color in colors" 
      :key="color"
      class="color-option"
      :style="{ backgroundColor: color }"
      :class="{ active: modelValue === color }"
      @click="selectColor(color)"
    />
  </div>
</template>

<script setup>
import { useCustomFieldValue } from '@vant/use';

const props = defineProps({
  modelValue: {
    type: String,
    default: '#000000',
  },
});

const emit = defineEmits(['update:modelValue']);

const colors = [
  '#000000', '#ffffff', '#ff0000', '#00ff00', 
  '#0000ff', '#ffff00', '#ff00ff', '#00ffff'
];

const selectColor = (color) => {
  emit('update:modelValue', color);
};

useCustomFieldValue(() => props.modelValue);
</script>

<style scoped>
.color-picker {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.color-option {
  width: 32px;
  height: 32px;
  border-radius: 4px;
  border: 2px solid transparent;
  cursor: pointer;
}

.color-option.active {
  border-color: #1989fa;
}
</style>
```

### Tag Selector Input

```vue
<template>
  <div class="tag-selector">
    <van-tag 
      v-for="tag in options"
      :key="tag"
      :type="selectedTags.includes(tag) ? 'primary' : 'default'"
      size="medium"
      @click="toggleTag(tag)"
    >
      {{ tag }}
    </van-tag>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';
import { useCustomFieldValue } from '@vant/use';

const props = defineProps({
  modelValue: {
    type: Array,
    default: () => [],
  },
  options: {
    type: Array,
    default: () => [],
  },
});

const emit = defineEmits(['update:modelValue']);

const selectedTags = ref([...props.modelValue]);

const toggleTag = (tag) => {
  const index = selectedTags.value.indexOf(tag);
  if (index > -1) {
    selectedTags.value.splice(index, 1);
  } else {
    selectedTags.value.push(tag);
  }
  emit('update:modelValue', [...selectedTags.value]);
};

watch(() => props.modelValue, (val) => {
  selectedTags.value = [...val];
});

useCustomFieldValue(() => selectedTags.value);
</script>

<style scoped>
.tag-selector {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}
</style>
```

### With Form Validation

```vue
<template>
  <van-form @submit="onSubmit" @failed="onFailed">
    <van-field 
      name="customNumber" 
      label="Number (1-10)"
      :rules="[{ required: true, message: 'Please select a number' }]"
    >
      <template #input>
        <number-slider v-model="formData.customNumber" />
      </template>
    </van-field>
    
    <div style="margin: 16px;">
      <van-button round block type="primary" native-type="submit">
        Submit
      </van-button>
    </div>
  </van-form>
</template>

<script setup>
import { reactive } from 'vue';
import { showToast } from 'vant';

const formData = reactive({
  customNumber: 5,
});

const onSubmit = (values) => {
  console.log('Form values:', values);
  showToast('Submitted successfully');
};

const onFailed = (errorInfo) => {
  console.log('Validation failed:', errorInfo);
};
</script>
```

## Best Practices

1. **Return Reactive Value**: Always return a reactive value from the getter function
2. **Use with van-field**: Place custom component in the `#input` slot of van-field
3. **Form Validation**: Works seamlessly with van-form validation rules
4. **v-model Support**: Implement v-model in your custom component for better usability
5. **Type Consistency**: Return consistent types for form processing
