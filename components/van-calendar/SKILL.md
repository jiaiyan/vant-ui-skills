---
name: "van-calendar"
description: "Calendar component for selecting dates or date ranges. Invoke when user needs to implement date selection, date range selection, or custom calendar views."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Calendar Component

Calendar component for selecting dates or date ranges with multiple selection modes.

## When to Invoke

Invoke this skill when:
- User needs to select a single date
- User wants to select multiple dates
- User needs to select a date range
- User wants to customize calendar appearance
- User asks about date formatting or validation
- User needs to limit date selection range

## Features

- **Multiple Selection Modes**: single, multiple, range
- **Switch Modes**: none, month, year-month for navigation
- **Custom Date Range**: min-date and max-date constraints
- **Custom Styling**: color customization, formatter support
- **Quick Select**: hide confirm button for immediate selection
- **Tiled Display**: inline display without popup
- **Custom Day Content**: top info, bottom info, custom text
- **Accessibility**: safe area adaptation, keyboard support

## API Reference

### Props

| Attribute | Description | Type | Default |
|-----------|-------------|------|---------|
| type | Type, can be set to `range` `multiple` | `string` | `single` |
| switch-mode | Switch mode: `none`, `month`, `year-month` | `string` | `none` |
| title | Title of calendar | `string` | `Calendar` |
| color | Color for the bottom button and selected date | `string` | `#1989fa` |
| min-date | Min date | `Date` | Today (when switch-mode is none) |
| max-date | Max date | `Date` | Six months after today (when switch-mode is none) |
| default-date | Default selected date | `Date \| Date[] \| null` | Today |
| row-height | Row height | `number \| string` | `64` |
| formatter | Day formatter | `(day: Day) => Day` | - |
| poppable | Whether to show the calendar inside a popup | `boolean` | `true` |
| lazy-render | Whether to enable lazy render | `boolean` | `true` |
| show-mark | Whether to show background month mark | `boolean` | `true` |
| show-title | Whether to show title | `boolean` | `true` |
| show-subtitle | Whether to show subtitle | `boolean` | `true` |
| show-confirm | Whether to show confirm button | `boolean` | `true` |
| readonly | Whether to be readonly | `boolean` | `false` |
| confirm-text | Confirm button text | `string` | `Confirm` |
| confirm-disabled-text | Confirm button text when disabled | `string` | `Confirm` |
| first-day-of-week | Set the start day of week | `0-6` | `0` |

### Calendar Poppable Props

| Attribute | Description | Type | Default |
|-----------|-------------|------|---------|
| v-model:show | Whether to show calendar | `boolean` | `false` |
| position | Popup position, can be set to `top` `right` `left` | `string` | `bottom` |
| round | Whether to show round corner | `boolean` | `true` |
| close-on-popstate | Whether to close when popstate | `boolean` | `true` |
| close-on-click-overlay | Whether to close when overlay is clicked | `boolean` | `true` |
| safe-area-inset-top | Whether to enable top safe area adaptation | `boolean` | `false` |
| safe-area-inset-bottom | Whether to enable bottom safe area adaptation | `boolean` | `true` |
| teleport | Specifies a target element where Calendar will be mounted | `string \| Element` | - |

### Calendar Range Props

| Attribute | Description | Type | Default |
|-----------|-------------|------|---------|
| max-range | Number of selectable days | `number \| string` | Unlimited |
| range-prompt | Error message when exceeded max range | `string` | `Choose no more than xx days` |
| show-range-prompt | Whether prompt error message when exceeded max range | `boolean` | `true` |
| allow-same-day | Whether the start and end time of the range is allowed on the same day | `boolean` | `false` |

### Calendar Multiple Props

| Attribute | Description | Type | Default |
|-----------|-------------|------|---------|
| max-range | Max count of selectable days | `number \| string` | Unlimited |
| range-prompt | Error message when exceeded max count | `string` | `Choose no more than xx days` |

### Data Structure of Day

| Key | Description | Type |
|-----|-------------|------|
| date | Date | `Date` |
| type | Type: `selected`, `start`, `middle`, `end`, `disabled`, `start-end`, `multiple-selected`, `multiple-middle`, `placeholder` | `string` |
| text | Text | `string` |
| topInfo | Top info | `string` |
| bottomInfo | Bottom info | `string` |
| className | Extra className | `string` |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| select | Emitted when date is selected | `value: Date \| Date[]` |
| confirm | Emitted after date selection is complete | `value: Date \| Date[]` |
| open | Emitted when opening Popup | - |
| close | Emitted when closing Popup | - |
| opened | Emitted when Popup is opened | - |
| closed | Emitted when Popup is closed | - |
| unselect | Emitted when unselect date when type is multiple | `value: Date` |
| month-show | Emitted when a month enters the visible area | `{ date: Date, title: string }` |
| over-range | Emitted when exceeded max range | - |
| click-subtitle | Emitted when clicking the subtitle | `event: MouseEvent` |
| click-disabled-date | Emitted when clicking disabled date | `value: Date \| Date[]` |
| click-overlay | Emitted when overlay is clicked | `event: MouseEvent` |
| panel-change | Emitted when switching calendar panel | `{ date: Date }` |

### Slots

| Name | Description | SlotProps |
|------|-------------|-----------|
| title | Custom title | - |
| subtitle | Custom subtitle | `{ text: string, date?: Date }` |
| month-title | Custom title of every month | `{ text: string, date: Date }` |
| footer | Custom footer | - |
| confirm-text | Custom confirm text | `{ disabled: boolean }` |
| top-info | Custom top info of day | `day: Day` |
| bottom-info | Custom bottom info of day | `day: Day` |
| text | Custom text of day | `day: Day` |
| prev-month | Custom previous month button | `{ disabled: boolean }` |
| prev-year | Custom previous year button | `{ disabled: boolean }` |
| next-month | Custom next month button | `{ disabled: boolean }` |
| next-year | Custom next year button | `{ disabled: boolean }` |

### Methods

Use ref to get Calendar instance and call instance methods.

| Name | Description | Attribute | Return value |
|------|-------------|-----------|--------------|
| reset | Reset selected date, will reset to default date when no params passed | `date?: Date \| Date[]` | - |
| scrollToDate | Scroll to date | `date: Date` | - |
| getSelectedDate | get selected date | - | `Date \| Date[] \| null` |

## Usage Examples

### Select Single Date

```vue
<template>
  <van-cell title="Select Single Date" :value="date" @click="show = true" />
  <van-calendar v-model:show="show" @confirm="onConfirm" />
</template>

<script setup>
import { ref } from 'vue'

const date = ref('')
const show = ref(false)

const formatDate = (date) => {
  return `${date.getFullYear()}/${date.getMonth() + 1}/${date.getDate()}`
}

const onConfirm = (value) => {
  show.value = false
  date.value = formatDate(value)
}
</script>
```

### Select Date Range

```vue
<template>
  <van-cell title="Select Date Range" :value="date" @click="show = true" />
  <van-calendar v-model:show="show" type="range" @confirm="onConfirm" />
</template>

<script setup>
import { ref } from 'vue'

const date = ref('')
const show = ref(false)

const formatDate = (date) => `${date.getMonth() + 1}/${date.getDate()}`

const onConfirm = (values) => {
  const [start, end] = values
  show.value = false
  date.value = `${formatDate(start)} - ${formatDate(end)}`
}
</script>
```

### Select Multiple Dates

```vue
<template>
  <van-cell title="Select Multiple Date" :value="text" @click="show = true" />
  <van-calendar v-model:show="show" type="multiple" @confirm="onConfirm" />
</template>

<script setup>
import { ref } from 'vue'

const text = ref('')
const show = ref(false)

const onConfirm = (dates) => {
  show.value = false
  text.value = `${dates.length} dates selected`
}
</script>
```

### Custom Date Range

```vue
<template>
  <van-calendar v-model:show="show" :min-date="minDate" :max-date="maxDate" />
</template>

<script setup>
import { ref } from 'vue'

const show = ref(false)
const minDate = new Date(2010, 0, 1)
const maxDate = new Date(2010, 0, 31)
</script>
```

### Custom Day Text

```vue
<template>
  <van-calendar v-model:show="show" type="range" :formatter="formatter" />
</template>

<script setup>
import { ref } from 'vue'

const show = ref(false)

const formatter = (day) => {
  const month = day.date.getMonth() + 1
  const date = day.date.getDate()

  if (month === 5) {
    if (date === 1) {
      day.topInfo = 'Labor Day'
    } else if (date === 4) {
      day.topInfo = 'Youth Day'
    } else if (date === 11) {
      day.text = 'Today'
    }
  }

  if (day.type === 'start') {
    day.bottomInfo = 'In'
  } else if (day.type === 'end') {
    day.bottomInfo = 'Out'
  }

  return day
}
</script>
```

### Quick Select

```vue
<template>
  <van-calendar v-model:show="show" :show-confirm="false" />
</template>

<script setup>
import { ref } from 'vue'

const show = ref(false)
</script>
```

### Tiled Display

```vue
<template>
  <van-calendar
    title="Calendar"
    :poppable="false"
    :show-confirm="false"
    :style="{ height: '500px' }"
  />
</template>
```

### Switch Mode

```vue
<template>
  <van-calendar v-model:show="show" switch-mode="year-month" />
</template>

<script setup>
import { ref } from 'vue'

const show = ref(false)
</script>
```

## Best Practices

1. **Date Format on iOS**: Avoid using `new Date('2020-01-01')` on iOS. Use `new Date('2020/01/01')` or `new Date(2020, 0, 1)` instead.

2. **Async Data in Formatter**: Use computed properties to dynamically create formatter functions when working with async data.

3. **Performance**: Use `switch-mode` when displaying many months to improve performance.

4. **Max Range**: Set `max-range` for range selection to prevent excessive date selection.

5. **Custom Styling**: Use `color` prop for simple color changes, or CSS variables for advanced customization.

6. **Accessibility**: Always provide clear labels and consider screen reader users when customizing calendar content.
