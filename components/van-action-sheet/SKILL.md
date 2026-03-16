---
name: "van-action-sheet"
description: "Action sheet component for displaying a bottom modal panel with multiple options. Invoke when user needs to implement action selection menus, option lists, or custom bottom panels."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant ActionSheet Component

A bottom modal panel component containing multiple options related to the current situation, commonly used for action selection.

## When to Invoke

Invoke this skill when:
- User needs to implement an action selection menu from the bottom
- User wants to display a list of options for user to choose
- User needs to show contextual actions related to specific content
- User wants to create a custom bottom panel with content
- User asks about implementing share menus or action menus

## Features

- **Multiple Options**: Display a list of actionable options
- **Icons Support**: Each option can have an icon
- **Option States**: Support loading, disabled, and colored options
- **Cancel Button**: Optional cancel button at the bottom
- **Description**: Support description text above options
- **Custom Content**: Full customization through slots
- **Safe Area**: Automatic bottom safe area adaptation
- **Teleport**: Support mounting to specified element

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model:show | Whether to show ActionSheet | `boolean` | `false` |
| actions | Options array | `ActionSheetAction[]` | `[]` |
| title | Title | `string` | - |
| cancel-text | Text of cancel button | `string` | - |
| description | Description above the options | `string` | - |
| closeable | Whether to show close icon | `boolean` | `true` |
| close-icon | Close icon name | `string` | `cross` |
| duration | Transition duration, unit second | `number \| string` | `0.3` |
| z-index | Set the z-index to a fixed value | `number \| string` | `2000+` |
| round | Whether to show round corner | `boolean` | `true` |
| overlay | Whether to show overlay | `boolean` | `true` |
| overlay-class | Custom overlay class | `string \| Array \| object` | - |
| overlay-style | Custom overlay style | `object` | - |
| lock-scroll | Whether to lock background scroll | `boolean` | `true` |
| lazy-render | Whether to lazy render until appeared | `boolean` | `true` |
| close-on-popstate | Whether to close when popstate | `boolean` | `true` |
| close-on-click-action | Whether to close when an action is clicked | `boolean` | `false` |
| close-on-click-overlay | Whether to close when overlay is clicked | `boolean` | `true` |
| safe-area-inset-bottom | Whether to enable bottom safe area adaptation | `boolean` | `true` |
| teleport | Specifies a target element where ActionSheet will be mounted | `string \| Element` | - |
| before-close | Callback function before close | `(action: string) => boolean \| Promise<boolean>` | - |

### ActionSheetAction Data Structure

| Key | Description | Type |
|-----|-------------|------|
| name | Title | `string` |
| subname | Subtitle | `string` |
| color | Text color | `string` |
| icon | Icon name or URL | `string` |
| className | className for the option | `string \| Array \| object` |
| loading | Whether to be loading status | `boolean` |
| disabled | Whether to be disabled | `boolean` |
| callback | Callback function after clicked | `action: ActionSheetAction` |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| select | Emitted when an option is clicked | `action: ActionSheetAction, index: number` |
| cancel | Emitted when the cancel button is clicked | - |
| open | Emitted when opening ActionSheet | - |
| close | Emitted when closing ActionSheet | - |
| opened | Emitted when ActionSheet is opened | - |
| closed | Emitted when ActionSheet is closed | - |
| click-overlay | Emitted when overlay is clicked | `event: MouseEvent` |

### Slots

| Name | Description | SlotProps |
|------|-------------|-----------|
| default | Custom content | - |
| description | Custom description above the options | - |
| cancel | Custom the content of cancel button | - |
| action | Custom the content of action | `{ action: ActionSheetAction, index: number }` |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-cell is-link title="Basic Usage" @click="show = true" />
  <van-action-sheet v-model:show="show" :actions="actions" @select="onSelect" />
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const show = ref(false)
const actions = [
  { name: 'Option 1' },
  { name: 'Option 2' },
  { name: 'Option 3' }
]

const onSelect = (item) => {
  show.value = false
  showToast(item.name)
}
</script>
```

### With Icons

```vue
<template>
  <van-cell is-link title="Show Icon" @click="show = true" />
  <van-action-sheet v-model:show="show" :actions="actions" @select="onSelect" />
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const show = ref(false)
const actions = [
  { name: 'Option 1', icon: 'cart-o' },
  { name: 'Option 2', icon: 'shop-o' },
  { name: 'Option 3', icon: 'star-o' }
]

const onSelect = (item) => {
  show.value = false
  showToast(item.name)
}
</script>
```

### With Cancel Button

```vue
<template>
  <van-action-sheet
    v-model:show="show"
    :actions="actions"
    cancel-text="Cancel"
    close-on-click-action
    @cancel="onCancel"
  />
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const show = ref(false)
const actions = [
  { name: 'Option 1' },
  { name: 'Option 2' },
  { name: 'Option 3' }
]

const onCancel = () => showToast('cancel')
</script>
```

### Option Status

```vue
<template>
  <van-action-sheet
    v-model:show="show"
    :actions="actions"
    cancel-text="Cancel"
    close-on-click-action
  />
</template>

<script setup>
import { ref } from 'vue'

const show = ref(false)
const actions = [
  { name: 'Colored Option', color: '#ee0a24' },
  { name: 'Disabled Option', disabled: true },
  { name: 'Loading Option', loading: true }
]
</script>
```

### Custom Panel

```vue
<template>
  <van-action-sheet v-model:show="show" title="Title">
    <div class="content">Custom content here</div>
  </van-action-sheet>
</template>

<script setup>
import { ref } from 'vue'

const show = ref(false)
</script>

<style scoped>
.content {
  padding: 16px 16px 160px;
}
</style>
```

## Common Issues

### 1. ActionSheet Not Closing After Selection

Set `close-on-click-action` to `true` or manually set `show` to `false`:

```vue
<van-action-sheet v-model:show="show" :actions="actions" close-on-click-action />
```

### 2. Custom Styling for Options

Use the `className` property in actions:

```js
const actions = [
  { name: 'Special Option', className: 'custom-option' }
]
```

### 3. Async Close Before Action

Use `before-close` callback:

```vue
<van-action-sheet v-model:show="show" :actions="actions" :before-close="beforeClose" />

<script setup>
const beforeClose = (action) => {
  return new Promise((resolve) => {
    setTimeout(() => resolve(true), 1000)
  })
}
</script>
```

## Component Interactions

### With Cell Component

```vue
<template>
  <van-cell-group>
    <van-cell is-link title="Edit Profile" @click="showActions('edit')" />
    <van-cell is-link title="Settings" @click="showActions('settings')" />
  </van-cell-group>
  
  <van-action-sheet v-model:show="show" :actions="currentActions" />
</template>
```

### With Toast Feedback

```vue
<template>
  <van-action-sheet v-model:show="show" :actions="actions" @select="onSelect" />
</template>

<script setup>
import { showToast } from 'vant'

const onSelect = (item) => {
  show.value = false
  showToast(`Selected: ${item.name}`)
}
</script>
```

## Best Practices

1. **Limit options**: Keep the number of options reasonable (3-7) for better UX
2. **Clear naming**: Use clear and concise option names
3. **Destructive actions**: Use red color for destructive actions like delete
4. **Loading state**: Show loading state for async operations
5. **Cancel option**: Always provide a way to cancel the action
6. **Safe area**: Keep `safe-area-inset-bottom` enabled for iOS devices
