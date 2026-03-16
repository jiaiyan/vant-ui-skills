---
name: "van-time-picker"
description: "Time picker component for selecting time. Invoke when user needs to implement time selection, time range selection, or custom time formats."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant TimePicker Component

Time picker component for selecting time with customizable columns and formatting.

## When to Invoke

Invoke this skill when:
- User needs to implement time selection
- User wants to create time range pickers
- User needs to filter or format time options
- User wants to customize time picker columns
- User asks about time picker with popup integration

## Features

- **Flexible Columns**: Select hour, minute, second individually
- **Time Range**: Limit selectable time range
- **Custom Formatting**: Format option text display
- **Option Filtering**: Filter available time options
- **Toolbar Customization**: Customizable toolbar and buttons
- **Popup Integration**: Works with Popup component
- **Readonly Mode**: Display without interaction
- **Loading State**: Show loading indicator

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model | Current time | `string[]` | - |
| columns-type | Columns type | `string[]` | `['hour', 'minute']` |
| min-hour | Min hour | `number \| string` | `0` |
| max-hour | Max hour | `number \| string` | `23` |
| min-minute | Min minute | `number \| string` | `0` |
| max-minute | Max minute | `number \| string` | `59` |
| min-second | Min second | `number \| string` | `0` |
| max-second | Max second | `number \| string` | `59` |
| min-time | Min time, format: `07:40:00` | `string` | - |
| max-time | Max time, format: `10:20:00` | `string` | - |
| title | Toolbar title | `string` | `''` |
| confirm-button-text | Text of confirm button | `string` | `Confirm` |
| cancel-button-text | Text of cancel button | `string` | `Cancel` |
| show-toolbar | Whether to show toolbar | `boolean` | `true` |
| loading | Whether to show loading prompt | `boolean` | `false` |
| readonly | Whether to be readonly | `boolean` | `false` |
| filter | Option filter | `(type: string, options: PickerOption[], values: string[]) => PickerOption[]` | - |
| formatter | Option text formatter | `(type: string, option: PickerOption) => PickerOption` | - |
| option-height | Option height | `number \| string` | `44` |
| visible-option-num | Count of visible columns | `number \| string` | `6` |
| swipe-duration | Duration of the momentum animation | `number \| string` | `1000` |

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

| Name | Description | Attribute | Return value |
|------|-------------|-----------|--------------|
| confirm | Stop scrolling and emit confirm event | - | - |
| getSelectedTime | Get current selected time | - | `string[]` |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-time-picker v-model="currentTime" title="Choose Time" />
</template>

<script setup>
import { ref } from 'vue'

const currentTime = ref(['12', '00'])
</script>
```

### Columns Type

```vue
<template>
  <van-time-picker
    v-model="currentTime"
    title="Choose Time"
    :columns-type="columnsType"
  />
</template>

<script setup>
import { ref } from 'vue'

const currentTime = ref(['12', '00', '00'])
const columnsType = ['hour', 'minute', 'second']
</script>
```

### Time Range

```vue
<template>
  <van-time-picker
    v-model="currentTime"
    title="Choose Time"
    :min-hour="10"
    :max-hour="20"
    :min-minute="30"
    :max-minute="40"
  />
</template>

<script setup>
import { ref } from 'vue'

const currentTime = ref(['12', '35'])
</script>
```

### Overall Time Range

```vue
<template>
  <van-time-picker
    v-model="currentTime"
    title="Choose Time"
    :columns-type="['hour', 'minute', 'second']"
    min-time="09:40:10"
    max-time="20:20:50"
  />
</template>

<script setup>
import { ref } from 'vue'

const currentTime = ref(['12', '00', '00'])
</script>
```

### Options Formatter

```vue
<template>
  <van-time-picker
    v-model="currentTime"
    title="Choose Time"
    :formatter="formatter"
  />
</template>

<script setup>
import { ref } from 'vue'

const currentTime = ref(['12', '00'])

const formatter = (type, option) => {
  if (type === 'hour') {
    option.text += 'h'
  }
  if (type === 'minute') {
    option.text += 'm'
  }
  return option
}
</script>
```

### Options Filter

```vue
<template>
  <van-time-picker 
    v-model="currentTime" 
    title="Choose Time" 
    :filter="filter" 
  />
</template>

<script setup>
import { ref } from 'vue'

const currentTime = ref(['12', '00'])

const filter = (type, options) => {
  if (type === 'minute') {
    return options.filter((option) => Number(option.value) % 10 === 0)
  }
  return options
}
</script>
```

### Advanced Filtering

```vue
<template>
  <van-time-picker title="Choose Time" :filter="filter" />
</template>

<script setup>
const filter = (type, options, values) => {
  const hour = +values[0]

  if (type === 'hour') {
    return options.filter(
      (option) => Number(option.value) >= 8 && Number(option.value) <= 18
    )
  }

  if (type === 'minute') {
    options = options.filter((option) => Number(option.value) % 10 === 0)

    if (hour === 8) {
      return options.filter((option) => Number(option.value) >= 40)
    }

    if (hour === 18) {
      return options.filter((option) => Number(option.value) <= 20)
    }
  }

  return options
}
</script>
```

### With Popup

```vue
<template>
  <div>
    <van-field
      v-model="timeDisplay"
      is-link
      readonly
      label="Time"
      placeholder="Select time"
      @click="showPicker = true"
    />
    <van-popup v-model:show="showPicker" position="bottom" round>
      <van-time-picker
        v-model="currentTime"
        title="Choose Time"
        @confirm="onConfirm"
        @cancel="showPicker = false"
      />
    </van-popup>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const currentTime = ref(['12', '00'])
const showPicker = ref(false)

const timeDisplay = computed(() => {
  return currentTime.value.join(':')
})

const onConfirm = () => {
  showPicker.value = false
}
</script>
```

### With Form

```vue
<template>
  <van-form @submit="onSubmit">
    <van-field
      v-model="timeDisplay"
      is-link
      readonly
      name="time"
      label="Time"
      placeholder="Select time"
      @click="showPicker = true"
    />
    <van-popup v-model:show="showPicker" position="bottom" round>
      <van-time-picker
        v-model="time"
        title="Select Time"
        @confirm="onTimeConfirm"
        @cancel="showPicker = false"
      />
    </van-popup>
    <div style="margin: 16px;">
      <van-button round block type="primary" native-type="submit">
        Submit
      </van-button>
    </div>
  </van-form>
</template>

<script setup>
import { ref, computed } from 'vue'
import { showToast } from 'vant'

const time = ref(['12', '00'])
const showPicker = ref(false)

const timeDisplay = computed(() => time.value.join(':'))

const onTimeConfirm = () => {
  showPicker.value = false
}

const onSubmit = () => {
  showToast('Selected time: ' + timeDisplay.value)
}
</script>
```

### Business Hours Picker

```vue
<template>
  <div class="business-hours">
    <van-cell-group inset>
      <van-cell title="Opening Time" is-link @click="openPicker('start')">
        {{ startTime.join(':') }}
      </van-cell>
      <van-cell title="Closing Time" is-link @click="openPicker('end')">
        {{ endTime.join(':') }}
      </van-cell>
    </van-cell-group>

    <van-popup v-model:show="showPicker" position="bottom" round>
      <van-time-picker
        v-model="selectedTime"
        :title="pickerTitle"
        :min-hour="minHour"
        :max-hour="maxHour"
        @confirm="onConfirm"
        @cancel="showPicker = false"
      />
    </van-popup>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const startTime = ref(['09', '00'])
const endTime = ref(['18', '00'])
const showPicker = ref(false)
const pickerType = ref('start')
const selectedTime = ref(['09', '00'])

const pickerTitle = computed(() => 
  pickerType.value === 'start' ? 'Opening Time' : 'Closing Time'
)

const minHour = computed(() => 
  pickerType.value === 'end' ? Number(startTime.value[0]) : 0
)

const maxHour = computed(() => 
  pickerType.value === 'start' ? Number(endTime.value[0]) : 23
)

const openPicker = (type) => {
  pickerType.value = type
  selectedTime.value = type === 'start' ? [...startTime.value] : [...endTime.value]
  showPicker.value = true
}

const onConfirm = () => {
  if (pickerType.value === 'start') {
    startTime.value = [...selectedTime.value]
  } else {
    endTime.value = [...selectedTime.value]
  }
  showPicker.value = false
}
</script>
```

## Best Practices

1. **Column Selection**: Choose appropriate columns for your use case
2. **Time Range**: Set reasonable min/max time constraints
3. **Formatting**: Use formatter for better user experience
4. **Filtering**: Filter options to prevent invalid selections
5. **Popup Integration**: Use with Popup for better mobile UX
6. **Validation**: Validate time selections in forms
7. **Default Values**: Set sensible default times
8. **Accessibility**: Provide clear labels and instructions
