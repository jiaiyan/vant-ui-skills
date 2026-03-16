---
name: "van-date-picker"
description: "Date picker component for selecting dates. Invoke when user needs to implement date selection with year, month, and day columns."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant DatePicker Component

Used to select date, usually used with the Popup component.

## When to Invoke

Invoke this skill when:
- User needs to select a date
- User wants to select year, month, or day separately
- User needs to customize date format
- User wants to filter or format date options
- User asks about date range constraints

## Features

- **Flexible Columns**: Select year, month, day, or any combination
- **Date Range**: Min and max date constraints
- **Custom Formatting**: Format option text
- **Option Filtering**: Filter available options
- **Toolbar**: Customizable toolbar with confirm and cancel
- **Loading State**: Show loading indicator for async data

## API Reference

### Props

| Attribute | Description | Type | Default |
|-----------|-------------|------|---------|
| v-model | Current date | `string[]` | `[]` |
| columns-type | Columns type | `string[]` | `['year', 'month', 'day']` |
| min-date | Min date | `Date` | Ten years ago on January 1 |
| max-date | Max date | `Date` | Ten years later on December 31 |
| title | Toolbar title | `string` | `''` |
| confirm-button-text | Text of confirm button | `string` | `Confirm` |
| cancel-button-text | Text of cancel button | `string` | `Cancel` |
| show-toolbar | Whether to show toolbar | `boolean` | `true` |
| loading | Whether to show loading prompt | `boolean` | `false` |
| readonly | Whether to be readonly | `boolean` | `false` |
| filter | Option filter | `(type: string, options: PickerOption[], values: string[]) => PickerOption[]` | - |
| formatter | Option formatter | `(type: string, option: PickerOption) => PickerOption` | - |
| option-height | Option height, supports `px` `vw` `vh` `rem` unit, default `px` | `number \| string` | `44` |
| visible-option-num | Count of visible columns | `number \| string` | `6` |
| swipe-duration | Duration of the momentum animation, unit `ms` | `number \| string` | `1000` |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| confirm | Emitted when the confirm button is clicked | `{ selectedValues, selectedOptions, selectedIndexes }` |
| cancel | Emitted when the cancel button is clicked | `{ selectedValues, selectedOptions, selectedIndexes }` |
| change | Emitted when current option is changed | `{ selectedValues, selectedOptions, selectedIndexes, columnIndex }` |

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

### Methods

Use ref to get DatePicker instance and call instance methods.

| Name | Description | Attribute | Return value |
|------|-------------|-----------|--------------|
| confirm | Stop scrolling and emit confirm event | - | - |
| getSelectedDate | Get current selected date | - | `string[]` |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-date-picker
    v-model="currentDate"
    title="Choose Date"
    :min-date="minDate"
    :max-date="maxDate"
  />
</template>

<script setup>
import { ref } from 'vue'

const currentDate = ref(['2021', '01', '01'])
const minDate = new Date(2020, 0, 1)
const maxDate = new Date(2025, 5, 1)
</script>
```

### Columns Type

```vue
<template>
  <van-date-picker
    v-model="currentDate"
    title="Choose Year-Month"
    :min-date="minDate"
    :max-date="maxDate"
    :columns-type="columnsType"
  />
</template>

<script setup>
import { ref } from 'vue'

const currentDate = ref(['2021', '01'])
const columnsType = ['year', 'month']
const minDate = new Date(2020, 0, 1)
const maxDate = new Date(2025, 5, 1)
</script>
```

### Options Formatter

```vue
<template>
  <van-date-picker
    v-model="currentDate"
    title="Choose Year-Month"
    :min-date="minDate"
    :max-date="maxDate"
    :formatter="formatter"
    :columns-type="columnsType"
  />
</template>

<script setup>
import { ref } from 'vue'

const currentDate = ref(['2021', '01'])
const columnsType = ['year', 'month']

const formatter = (type, option) => {
  if (type === 'year') {
    option.text += ' Year'
  }
  if (type === 'month') {
    option.text += ' Month'
  }
  return option
}

const minDate = new Date(2020, 0, 1)
const maxDate = new Date(2025, 5, 1)
</script>
```

### Options Filter

```vue
<template>
  <van-date-picker
    v-model="currentDate"
    title="Choose Year-Month"
    :filter="filter"
    :min-date="minDate"
    :max-date="maxDate"
    :columns-type="columnsType"
  />
</template>

<script setup>
import { ref } from 'vue'

const currentDate = ref(['2021', '01'])
const columnsType = ['year', 'month']

const filter = (type, options) => {
  if (type === 'month') {
    return options.filter((option) => Number(option.value) % 6 === 0)
  }
  return options
}

const minDate = new Date(2020, 0, 1)
const maxDate = new Date(2025, 5, 1)
</script>
```

### With Popup

```vue
<template>
  <van-field
    v-model="result"
    is-link
    readonly
    name="datePicker"
    label="Date Picker"
    placeholder="Select date"
    @click="showPicker = true"
  />
  <van-popup v-model:show="showPicker" destroy-on-close position="bottom">
    <van-date-picker
      :model-value="pickerValue"
      @confirm="onConfirm"
      @cancel="showPicker = false"
    />
  </van-popup>
</template>

<script setup>
import { ref } from 'vue'

const result = ref('')
const showPicker = ref(false)
const pickerValue = ref([])

const onConfirm = ({ selectedValues }) => {
  result.value = selectedValues.join('/')
  pickerValue.value = selectedValues
  showPicker.value = false
}
</script>
```

## Best Practices

1. **Date Range**: Always set appropriate `min-date` and `max-date` to constrain user selection.

2. **Columns Type**: Use `columns-type` to show only the columns you need (e.g., `['year', 'month']` for year-month selection).

3. **Formatter**: Use `formatter` to add units or customize option text for better user experience.

4. **Filter**: Use `filter` to restrict available options (e.g., only show specific months).

5. **With Popup**: Combine with Popup component for better mobile experience.

6. **v-model Format**: The v-model value is an array of strings in the format `['year', 'month', 'day']`.
