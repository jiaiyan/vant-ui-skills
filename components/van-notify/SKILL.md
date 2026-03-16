---
name: "van-notify"
description: "Notify component for displaying top notification messages. Invoke when user needs to implement toast notifications, alert messages, or temporary status indicators."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Notify Component

A notification component that displays messages at the top of the page, supporting both component and function call methods.

## When to Invoke

Invoke this skill when:
- User needs to display temporary notification messages
- User wants to show success/error/warning alerts
- User needs top-positioned toast notifications
- User asks about notification types or customization
- User wants to implement status feedback messages

## Features

- **Function Call**: Quick invocation via `showNotify`
- **Multiple Types**: Primary, success, warning, danger types
- **Custom Position**: Top or bottom positioning
- **Auto Close**: Configurable auto-close duration
- **Custom Styling**: Custom colors and background
- **Component Mode**: Full customization via component usage

## API Reference

### Methods

| Name | Description | Arguments | Return Value |
|------|-------------|-----------|--------------|
| showNotify | Display Notify at the top of the page | `NotifyOptions \| string` | Notify instance |
| closeNotify | Close the currently displayed Notify | - | `void` |
| setNotifyDefaultOptions | Modify default configuration | `NotifyOptions` | `void` |
| resetNotifyDefaultOptions | Reset default configuration | - | `void` |

### NotifyOptions

| Name | Description | Type | Default |
|------|-------------|------|---------|
| type | Type: `primary`, `success`, `warning` | `NotifyType` | `danger` |
| message | Message | `string` | - |
| duration | Duration(ms), won't disappear if 0 | `number \| string` | `3000` |
| zIndex | z-index | `number \| string` | `2000+` |
| position | Position, can be `bottom` | `NotifyPosition` | `top` |
| color | Message color | `string` | `white` |
| background | Background color | `string` | - |
| className | Custom className | `string \| Array \| object` | - |
| lockScroll | Whether to lock background scroll | `boolean` | `false` |
| teleport | Target element for mounting | `string \| Element` | - |
| onClick | Callback after click | `(event: MouseEvent) => void` | - |
| onOpened | Callback after opened | `() => void` | - |
| onClose | Callback after close | `() => void` | - |

### Props (Component Usage)

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model:show | Whether to show notify | `boolean` | `false` |
| type | Type | `NotifyType` | `danger` |
| message | Message | `string` | - |
| z-index | z-index | `number \| string` | `2000+` |
| position | Position | `NotifyPosition` | `top` |
| color | Message color | `string` | `white` |
| background | Background color | `string` | - |
| class-name | Custom className | `string \| Array \| object` | - |
| lock-scroll | Whether to lock background scroll | `boolean` | `false` |
| teleport | Target element for mounting | `string \| Element` | - |

### Events

| Event | Description | Parameters |
|-------|-------------|------------|
| click | Callback after click | `event: MouseEvent` |
| close | Callback after close | - |
| opened | Callback after opened | - |

### Slots

| Name | Description |
|------|-------------|
| default | Custom content |

### Types

```ts
import type { NotifyType, NotifyProps, NotifyOptions, NotifyPosition } from 'vant'
```

## Usage Examples

### Basic Usage

```vue
<script setup>
import { showNotify, closeNotify } from 'vant'

const showBasicNotify = () => {
  showNotify('Message')
}

const showAndClose = () => {
  showNotify('Message')
  setTimeout(() => closeNotify(), 1000)
}
</script>
```

### Notify Types

```vue
<script setup>
import { showNotify } from 'vant'

const showPrimary = () => showNotify({ type: 'primary', message: 'Primary' })
const showSuccess = () => showNotify({ type: 'success', message: 'Success' })
const showDanger = () => showNotify({ type: 'danger', message: 'Danger' })
const showWarning = () => showNotify({ type: 'warning', message: 'Warning' })
</script>
```

### Custom Styling

```vue
<script setup>
import { showNotify } from 'vant'

const showCustom = () => {
  showNotify({
    message: 'Custom Color',
    color: '#ad0000',
    background: '#ffe1e1'
  })
}

const showBottom = () => {
  showNotify({
    message: 'Bottom Position',
    position: 'bottom'
  })
}

const showShort = () => {
  showNotify({
    message: '1 Second Duration',
    duration: 1000
  })
}
</script>
```

### Component Usage

```vue
<template>
  <van-button type="primary" @click="showNotify">Show Notify</van-button>
  <van-notify v-model:show="show" type="success">
    <van-icon name="bell" style="margin-right: 4px;" />
    <span>Content</span>
  </van-notify>
</template>

<script setup>
import { ref } from 'vue'

const show = ref(false)

const showNotify = () => {
  show.value = true
  setTimeout(() => {
    show.value = false
  }, 2000)
}
</script>
```

### With Callbacks

```vue
<script setup>
import { showNotify } from 'vant'

const showWithCallback = () => {
  showNotify({
    message: 'Click me',
    onClick: () => {
      console.log('Notify clicked')
    },
    onOpened: () => {
      console.log('Notify opened')
    },
    onClose: () => {
      console.log('Notify closed')
    }
  })
}
</script>
```

## Common Issues

### 1. Notify Not Disappearing

Set `duration` to 0 for persistent notify, close manually:

```js
showNotify({ message: 'Persistent', duration: 0 })
setTimeout(() => closeNotify(), 5000)
```

### 2. Multiple Notifies Overlapping

Close previous notify before showing new one:

```js
const showSequential = () => {
  closeNotify()
  showNotify({ message: 'New message' })
}
```

### 3. Custom Type Colors

Use `background` and `color` for full customization:

```js
showNotify({
  message: 'Custom',
  background: '#07c160',
  color: '#fff'
})
```

## Component Interactions

### With Form Submission

```vue
<script setup>
import { showNotify } from 'vant'

const submitForm = async () => {
  try {
    await submitData()
    showNotify({ type: 'success', message: 'Submitted successfully' })
  } catch (error) {
    showNotify({ type: 'danger', message: 'Submission failed' })
  }
}
</script>
```

### With Network Status

```vue
<script setup>
import { showNotify, closeNotify } from 'vant'

watch(networkStatus, (status) => {
  if (!status.connected) {
    showNotify({
      type: 'warning',
      message: 'Network disconnected',
      duration: 0
    })
  } else {
    closeNotify()
    showNotify({ type: 'success', message: 'Network restored' })
  }
})
</script>
```

### With Action Confirmation

```vue
<script setup>
import { showNotify } from 'vant'

const deleteItem = (id) => {
  showNotify({
    type: 'danger',
    message: 'Item deleted',
    duration: 2000
  })
}
</script>
```

## Best Practices

1. **Appropriate duration**: Use 2-3 seconds for most messages
2. **Type selection**: Use appropriate type for context
3. **Concise messages**: Keep messages short and clear
4. **Avoid spamming**: Don't show too many notifies in succession
5. **Position consistency**: Stick to one position in your app
6. **Accessibility**: Ensure sufficient color contrast
