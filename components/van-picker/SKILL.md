---
name: "van-picker"
description: "Picker component for selecting values from a list. Invoke when user needs to implement single or multi-column selection, cascade selection, or custom picker views."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Picker Component

The picker component is usually used with Popup Component for selecting values from a list.

## When to Invoke

Invoke this skill when:
- User needs to select from a list of options
- User wants to implement multi-column selection
- User needs cascade selection (e.g., city selection)
- User wants to customize picker appearance
- User asks about loading state or disabled options

## Features

- **Single/Multiple Columns**: Support for single or multiple column selection
- **Cascade Selection**: Support for hierarchical data
- **Custom Field Names**: Customize text, value, and children fields
- **Loading State**: Show loading indicator for async data
- **Disabled Options**: Disable specific options
- **Custom Slots**: Multiple slots for customization
- **Toolbar**: Customizable toolbar with confirm and cancel

## API Reference

### Props

| Attribute | Description | Type | Default |
|-----------|-------------|------|---------|
| v-model | values of chosen option | `number[] \| string[]` | - |
| columns | Columns data | `PickerOption[] \| PickerOption[][]` | `[]` |
| columns-field-names | custom columns field | `object` | `{ text: 'text', value: 'value', children: 'children' }` |
| title | Toolbar title | `string` | - |
| confirm-button-text | Text of confirm button, setting it as an empty string can hide the button | `string` | `Confirm` |
| cancel-button-text | Text of cancel button, setting it as an empty string can hide the button | `string` | `Cancel` |
| toolbar-position | Toolbar position, cat be set to `bottom` | `string` | `top` |
| loading | Whether to show loading prompt | `boolean` | `false` |
| readonly | Whether to be readonly | `boolean` | `false` |
| show-toolbar | Whether to show toolbar | `boolean` | `true` |
| allow-html | Whether to allow HTML in option text | `boolean` | `false` |
| option-height | Option height, supports `px` `vw` `vh` `rem` unit, default `px` | `number \| string` | `44` |
| visible-option-num | Count of visible columns | `number \| string` | `6` |
| swipe-duration | Duration of the momentum animation, unit `ms` | `number \| string` | `1000` |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| confirm | Emitted when the confirm button is clicked | `{ selectedValues, selectedOptions, selectedIndexes }` |
| cancel | Emitted when the cancel button is clicked | `{ selectedValues, selectedOptions, selectedIndexes }` |
| change | Emitted when current selected option is changed | `{ selectedValues, selectedOptions, selectedIndexes, columnIndex }` |
| click-option | Emitted when an option is clicked | `{ currentOption, selectedValues, selectedOptions, selectedIndexes, columnIndex }` |
| scroll-into | Emitted when an option is scrolled into the middle selection area | `{ currentOption, columnIndex }` |

### Slots

| Name | Description | SlotProps |
|------|-------------|-----------|
| toolbar | Custom toolbar content | - |
| title | Custom title | - |
| confirm | Custom confirm button text | - |
| cancel | Custom cancel button text | - |
| option | Custom option content | `option: PickerOption, index: number` |
| columns-top | Custom content above columns | - |
| columns-bottom | Custom content below columns | - |
| empty | Custom empty content | - |

### Data Structure of PickerOption

| Key | Description | Type |
|-----|-------------|------|
| text | Text | `string \| number` |
| value | Value of option | `string \| number` |
| disabled | Whether to disable option | `boolean` |
| children | Cascade children options | `PickerOption[]` |
| className | ClassName for this option | `string \| Array \| object` |

### Methods

Use ref to get Picker instance and call instance methods.

| Name | Description | Attribute | Return value |
|------|-------------|-----------|--------------|
| confirm | Stop scrolling and emit confirm event | - | - |
| getSelectedOptions | Get current selected options | - | `(PickerOption \| undefined)[]` |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-picker
    title="Title"
    :columns="columns"
    @confirm="onConfirm"
    @cancel="onCancel"
    @change="onChange"
  />
</template>

<script setup>
import { showToast } from 'vant'

const columns = [
  { text: 'Delaware', value: 'Delaware' },
  { text: 'Florida', value: 'Florida' },
  { text: 'Wenzhou', value: 'Wenzhou' },
  { text: 'Indiana', value: 'Indiana' },
  { text: 'Maine', value: 'Maine' },
]

const onConfirm = ({ selectedValues }) => {
  showToast(`Value: ${selectedValues.join(',')}`)
}

const onChange = ({ selectedValues }) => {
  showToast(`Value: ${selectedValues.join(',')}`)
}

const onCancel = () => showToast('Cancel')
</script>
```

### With Popup

```vue
<template>
  <van-field
    v-model="fieldValue"
    is-link
    readonly
    label="City"
    placeholder="Choose City"
    @click="showPicker = true"
  />
  <van-popup v-model:show="showPicker" destroy-on-close round position="bottom">
    <van-picker
      :model-value="pickerValue"
      title="Title"
      :columns="columns"
      @cancel="showPicker = false"
      @confirm="onConfirm"
    />
  </van-popup>
</template>

<script setup>
import { ref } from 'vue'

const columns = [
  { text: 'Delaware', value: 'Delaware' },
  { text: 'Florida', value: 'Florida' },
  { text: 'Wenzhou', value: 'Wenzhou' },
]

const fieldValue = ref('')
const pickerValue = ref([])
const showPicker = ref(false)

const onConfirm = ({ selectedValues, selectedOptions }) => {
  showPicker.value = false
  pickerValue.value = selectedValues
  fieldValue.value = selectedOptions[0].text
}
</script>
```

### v-model

```vue
<template>
  <van-picker v-model="selectedValues" title="Title" :columns="columns" />
</template>

<script setup>
import { ref } from 'vue'

const columns = [
  { text: 'Delaware', value: 'Delaware' },
  { text: 'Florida', value: 'Florida' },
  { text: 'Wenzhou', value: 'Wenzhou' },
]

const selectedValues = ref(['Wenzhou'])
</script>
```

### Multiple Columns

```vue
<template>
  <van-picker title="Title" :columns="columns" />
</template>

<script setup>
const columns = [
  [
    { text: 'Monday', value: 'Monday' },
    { text: 'Tuesday', value: 'Tuesday' },
    { text: 'Wednesday', value: 'Wednesday' },
    { text: 'Thursday', value: 'Thursday' },
    { text: 'Friday', value: 'Friday' },
  ],
  [
    { text: 'Morning', value: 'Morning' },
    { text: 'Afternoon', value: 'Afternoon' },
    { text: 'Evening', value: 'Evening' },
  ],
]
</script>
```

### Cascade

```vue
<template>
  <van-picker title="Title" :columns="columns" />
</template>

<script setup>
const columns = [
  {
    text: 'Zhejiang',
    value: 'Zhejiang',
    children: [
      {
        text: 'Hangzhou',
        value: 'Hangzhou',
        children: [
          { text: 'Xihu', value: 'Xihu' },
          { text: 'Yuhang', value: 'Yuhang' },
        ],
      },
      {
        text: 'Wenzhou',
        value: 'Wenzhou',
        children: [
          { text: 'Lucheng', value: 'Lucheng' },
          { text: 'Ouhai', value: 'Ouhai' },
        ],
      },
    ],
  },
  {
    text: 'Fujian',
    value: 'Fujian',
    children: [
      {
        text: 'Fuzhou',
        value: 'Fuzhou',
        children: [
          { text: 'Gulou', value: 'Gulou' },
          { text: 'Taijiang', value: 'Taijiang' },
        ],
      },
      {
        text: 'Xiamen',
        value: 'Xiamen',
        children: [
          { text: 'Siming', value: 'Siming' },
          { text: 'Haicang', value: 'Haicang' },
        ],
      },
    ],
  },
]
</script>
```

### Disable Option

```vue
<template>
  <van-picker :columns="columns" />
</template>

<script setup>
const columns = [
  { text: 'Delaware', value: 'Delaware', disabled: true },
  { text: 'Florida', value: 'Florida' },
  { text: 'Wenzhou', value: 'Wenzhou' },
]
</script>
```

### Loading

```vue
<template>
  <van-picker title="Title" :columns="columns" :loading="loading" />
</template>

<script setup>
import { ref } from 'vue'

const columns = ref([])
const loading = ref(true)

setTimeout(() => {
  columns.value = [{ text: 'Option', value: 'option' }]
  loading.value = false
}, 1000)
</script>
```

### Empty Content

```vue
<template>
  <van-picker title="Title">
    <template #empty>
      <van-empty
        image="https://fastly.jsdelivr.net/npm/@vant/assets/custom-empty-image.png"
        image-size="80"
        description="No data"
      />
    </template>
  </van-picker>
</template>
```

### Custom Columns Field

```vue
<template>
  <van-picker
    title="Title"
    :columns="columns"
    :columns-field-names="customFieldName"
  />
</template>

<script setup>
const columns = [
  {
    cityName: 'Zhejiang',
    cities: [
      {
        cityName: 'Hangzhou',
        cities: [{ cityName: 'Xihu' }, { cityName: 'Yuhang' }],
      },
      {
        cityName: 'Wenzhou',
        cities: [{ cityName: 'Lucheng' }, { cityName: 'Ouhai' }],
      },
    ],
  },
]

const customFieldName = {
  text: 'cityName',
  value: 'cityName',
  children: 'cities',
}
</script>
```

## Best Practices

1. **With Popup**: Always use with Popup component for better mobile experience.

2. **Cascade Data**: Use `children` property for cascade selection, or customize with `columns-field-names`.

3. **Loading State**: Show loading indicator when loading async data.

4. **Disabled Options**: Use `disabled` property to prevent selection of certain options.

5. **Custom Field Names**: Use `columns-field-names` when your data structure doesn't match the default.

6. **Empty State**: Provide custom empty content when there's no data.

7. **Performance**: For large datasets, consider loading data asynchronously.

8. **v-model**: Use v-model for two-way binding of selected values.
