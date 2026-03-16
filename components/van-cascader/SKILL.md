---
name: "van-cascader"
description: "Cascader component for multi-level data selection. Invoke when user needs to implement hierarchical selection like provinces and cities."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Cascader Component

Cascader component for multi-level data selection, typically used for province-city selection.

## When to Invoke

Invoke this skill when:
- User needs to select hierarchical data (e.g., provinces and cities)
- User wants to implement multi-level selection
- User needs to load options asynchronously
- User wants to customize field names
- User asks about cascading selection patterns

## Features

- **Multi-level Selection**: Support for unlimited levels
- **Async Options**: Load options dynamically
- **Custom Field Names**: Customize text, value, and children fields
- **Custom Styling**: Active color customization
- **Swipeable**: Gesture support for navigation
- **Custom Content**: Slots for custom rendering

## API Reference

### Props

| Attribute | Description | Type | Default |
|-----------|-------------|------|---------|
| v-model | Value of selected option | `string \| number` | - |
| title | Title | `string` | - |
| options | Options | `CascaderOption[]` | `[]` |
| placeholder | Placeholder of unselected tab | `string` | `Select` |
| active-color | Active color | `string` | `#1989fa` |
| swipeable | Whether to enable gestures to slide left and right | `boolean` | `true` |
| closeable | Whether to show close icon | `boolean` | `true` |
| show-header | Whether to show header | `boolean` | `true` |
| close-icon | Close icon name | `string` | `cross` |
| field-names | Custom the fields of options | `CascaderFieldNames` | `{ text: 'text', value: 'value', children: 'children' }` |

### Data Structure of CascaderOption

| Key | Description | Type |
|-----|-------------|------|
| text | Option text | `string` |
| value | Option value | `string \| number` |
| color | Text color | `string` |
| children | Cascade children | `CascaderOption[]` |
| disabled | Whether to disable option | `boolean` |
| className | className for the option | `string \| Array \| object` |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| change | Emitted when active option changed | `{ value: string \| number, selectedOptions: CascaderOption[], tabIndex: number }` |
| finish | Emitted when all options is selected | `{ value: string \| number, selectedOptions: CascaderOption[], tabIndex: number }` |
| close | Emitted when the close icon is clicked | - |
| click-tab | Emitted when a tab is clicked | `activeTab: number, title: string` |

### Slots

| Name | Description | SlotProps |
|------|-------------|-----------|
| title | Custom title | - |
| option | Custom option text | `{ option: CascaderOption, selected: boolean }` |
| options-top | Custom the content above the options | `{ tabIndex: number }` |
| options-bottom | Custom the content below the options | `{ tabIndex: number }` |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-field
    v-model="fieldValue"
    is-link
    readonly
    label="Area"
    placeholder="Select Area"
    @click="show = true"
  />
  <van-popup v-model="show" round position="bottom">
    <van-cascader
      v-model="cascaderValue"
      title="Select Area"
      :options="options"
      @close="show = false"
      @finish="onFinish"
    />
  </van-popup>
</template>

<script setup>
import { ref } from 'vue'

const show = ref(false)
const fieldValue = ref('')
const cascaderValue = ref('')

const options = [
  {
    text: 'Zhejiang',
    value: '330000',
    children: [{ text: 'Hangzhou', value: '330100' }],
  },
  {
    text: 'Jiangsu',
    value: '320000',
    children: [{ text: 'Nanjing', value: '320100' }],
  },
]

const onFinish = ({ selectedOptions }) => {
  show.value = false
  fieldValue.value = selectedOptions.map((option) => option.text).join('/')
}
</script>
```

### Custom Color

```vue
<template>
  <van-cascader
    v-model="cascaderValue"
    title="Select Area"
    :options="options"
    active-color="#ee0a24"
    @close="show = false"
    @finish="onFinish"
  />
</template>
```

### Async Options

```vue
<template>
  <van-field
    v-model="fieldValue"
    is-link
    readonly
    label="Area"
    placeholder="Select Area"
    @click="show = true"
  />
  <van-popup v-model="show" round position="bottom">
    <van-cascader
      v-model="cascaderValue"
      title="Select Area"
      :options="options"
      @close="show = false"
      @change="onChange"
      @finish="onFinish"
    />
  </van-popup>
</template>

<script setup>
import { ref } from 'vue'
import { closeToast, showLoadingToast } from 'vant'

const show = ref(false)
const fieldValue = ref('')
const cascaderValue = ref('')

const options = ref([
  {
    text: 'Zhejiang',
    value: '330000',
    children: [],
  },
])

const onChange = ({ value }) => {
  if (
    value === options.value[0].value &&
    options.value[0].children.length === 0
  ) {
    showLoadingToast('Loading...')
    setTimeout(() => {
      options.value[0].children = [
        { text: 'Hangzhou', value: '330100' },
        { text: 'Ningbo', value: '330200' },
      ]
      closeToast()
    }, 1000)
  }
}

const onFinish = ({ selectedOptions }) => {
  show.value = false
  fieldValue.value = selectedOptions.map((option) => option.text).join('/')
}
</script>
```

### Custom Field Names

```vue
<template>
  <van-cascader
    v-model="code"
    title="Select Area"
    :options="options"
    :field-names="fieldNames"
  />
</template>

<script setup>
import { ref } from 'vue'

const code = ref('')

const fieldNames = {
  text: 'name',
  value: 'code',
  children: 'items',
}

const options = [
  {
    name: 'Zhejiang',
    code: '330000',
    items: [{ name: 'Hangzhou', code: '330100' }],
  },
  {
    name: 'Jiangsu',
    code: '320000',
    items: [{ name: 'Nanjing', code: '320100' }],
  },
]
</script>
```

### Custom Content

```vue
<template>
  <van-cascader v-model="code" title="Select Area" :options="options">
    <template #options-top="{ tabIndex }">
      <div class="current-level">Current level is {{ tabIndex + 1 }}</div>
    </template>
  </van-cascader>
</template>

<style>
.current-level {
  font-size: 14px;
  padding: 16px 16px 0;
  color: var(--van-gray-6);
}
</style>
```

## Best Practices

1. **Async Loading**: Show loading indicator when fetching async data to improve user experience.

2. **Field Names**: Use `field-names` prop when your data structure doesn't match the default field names.

3. **Performance**: For large datasets, consider loading options asynchronously instead of loading all at once.

4. **Error Handling**: Handle async loading errors gracefully and provide feedback to users.

5. **Default Values**: Set appropriate default values to improve user experience.

6. **Mobile Optimization**: The component is optimized for mobile, ensure proper touch interactions.
