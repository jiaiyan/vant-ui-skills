---
name: "van-picker-group"
description: "Picker group component for combining multiple pickers. Invoke when user needs to select multiple values from different pickers, like date and time together."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant PickerGroup Component

Used to combine multiple Picker components, allow users to select multiple values.

## When to Invoke

Invoke this skill when:
- User needs to select date and time together
- User wants to select a date range
- User needs to select time range
- User wants to combine multiple pickers
- User asks about next step button functionality

## Features

- **Multiple Pickers**: Combine DatePicker, TimePicker, Picker, etc.
- **Unified Toolbar**: Single toolbar for all pickers
- **Tab Navigation**: Switch between pickers with tabs
- **Next Step Button**: Guide users through sequential selection
- **Controlled Mode**: Support for controlled tab switching
- **Custom Tabs**: Customizable tab titles

## API Reference

### Props

| Attribute | Description | Type | Default |
|-----------|-------------|------|---------|
| v-model:active-tab | Set index of active tab | `number \| string` | `0` |
| tabs | Titles of tabs | `string[]` | `[]` |
| title | Toolbar title | `string` | `''` |
| show-toolbar | Whether to show toolbar | `boolean` | `true` |
| next-step-text | Text of next step button | `string` | `''` |
| confirm-button-text | Text of confirm button | `string` | `Confirm` |
| cancel-button-text | Text of cancel button | `string` | `Cancel` |

### Slots

| Name | Description | SlotProps |
|------|-------------|-----------|
| toolbar | Custom toolbar content | - |
| title | Custom title | - |
| confirm | Custom confirm button text | - |
| cancel | Custom cancel button text | - |

## Usage Examples

### Select Date Time

```vue
<template>
  <van-picker-group
    title="Title"
    :tabs="['Date', 'Time']"
    @confirm="onConfirm"
    @cancel="onCancel"
  >
    <van-date-picker
      v-model="currentDate"
      :min-date="minDate"
      :max-date="maxDate"
    />
    <van-time-picker v-model="currentTime" />
  </van-picker-group>
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const currentDate = ref(['2022', '06', '01'])
const currentTime = ref(['12', '00'])

const onConfirm = () => {
  showToast(`${currentDate.value.join('/')} ${currentTime.value.join(':')}`)
}

const onCancel = () => {
  showToast('cancel')
}

const minDate = new Date(2020, 0, 1)
const maxDate = new Date(2025, 5, 1)
</script>
```

### Next Step Button

```vue
<template>
  <van-picker-group
    title="Title"
    :tabs="['Date', 'Time']"
    next-step-text="Next Step"
    @confirm="onConfirm"
    @cancel="onCancel"
  >
    <van-date-picker
      v-model="currentDate"
      :min-date="minDate"
      :max-date="maxDate"
    />
    <van-time-picker v-model="currentTime" />
  </van-picker-group>
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const currentDate = ref(['2022', '06', '01'])
const currentTime = ref(['12', '00'])

const onConfirm = () => {
  showToast(`${currentDate.value.join('/')} ${currentTime.value.join(':')}`)
}

const onCancel = () => {
  showToast('cancel')
}

const minDate = new Date(2020, 0, 1)
const maxDate = new Date(2025, 5, 1)
</script>
```

### Select Date Range

```vue
<template>
  <van-picker-group
    title="Title"
    :tabs="['Start Date', 'End Date']"
    @confirm="onConfirm"
    @cancel="onCancel"
  >
    <van-date-picker
      v-model="startDate"
      :min-date="minDate"
      :max-date="maxDate"
    />
    <van-date-picker
      v-model="endDate"
      :min-date="endMinDate"
      :max-date="maxDate"
    />
  </van-picker-group>
</template>

<script setup>
import { computed, ref } from 'vue'
import { showToast } from 'vant'

const startDate = ref(['2022', '06', '01'])
const endDate = ref(['2023', '06', '01'])

const endMinDate = computed(
  () =>
    new Date(
      Number(startDate.value[0]),
      Number(startDate.value[1]) - 1,
      Number(startDate.value[2]),
    ),
)

const onConfirm = () => {
  showToast(`${startDate.value.join('/')} ${endDate.value.join('/')}`)
}

const onCancel = () => {
  showToast('cancel')
}

const minDate = new Date(2020, 0, 1)
const maxDate = new Date(2025, 5, 1)
</script>
```

### Select Time Range

```vue
<template>
  <van-picker-group
    title="Title"
    :tabs="['Start Time', 'End Time']"
    @confirm="onConfirm"
    @cancel="onCancel"
  >
    <van-time-picker v-model="startTime" />
    <van-time-picker v-model="endTime" />
  </van-picker-group>
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const startTime = ref(['12', '00'])
const endTime = ref(['12', '00'])

const onConfirm = () => {
  showToast(`${startTime.value.join(':')} ${endTime.value.join(':')}`)
}

const onCancel = () => {
  showToast('cancel')
}
</script>
```

### Controlled Mode

```vue
<template>
  <van-button type="primary" @click="setActiveTab">
    toggle tab, current {{ activeTab }}
  </van-button>
  <van-picker-group
    v-model:active-tab="activeTab"
    title="Title"
    :tabs="['Date', 'Time']"
    @confirm="onConfirm"
    @cancel="onCancel"
  >
    <van-date-picker
      v-model="currentDate"
      :min-date="minDate"
      :max-date="maxDate"
    />
    <van-time-picker v-model="currentTime" />
  </van-picker-group>
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const activeTab = ref(0)
const currentDate = ref(['2022', '06', '01'])
const currentTime = ref(['12', '00'])

const setActiveTab = () => {
  activeTab.value = activeTab.value ? 0 : 1
}

const onConfirm = () => {
  showToast(`${currentDate.value.join('/')} ${currentTime.value.join(':')}`)
}

const onCancel = () => {
  showToast('cancel')
}

const minDate = new Date(2020, 0, 1)
const maxDate = new Date(2025, 5, 1)
</script>
```

## Best Practices

1. **Combine Related Pickers**: Use PickerGroup to combine related pickers like date and time.

2. **Next Step Button**: Use `next-step-text` to guide users through sequential selection.

3. **Controlled Mode**: Use `v-model:active-tab` for programmatic control of tab switching.

4. **Date Range**: Use computed properties to dynamically set min/max dates for end date picker.

5. **Tab Titles**: Provide clear and descriptive tab titles for better user experience.

6. **Toolbar**: The toolbar is rendered by PickerGroup, so don't set toolbar props on child pickers.

7. **Child Components**: The following components can be placed inside PickerGroup:
   - Picker
   - DatePicker
   - TimePicker
   - Area
   - Other custom components based on Picker
