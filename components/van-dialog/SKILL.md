---
name: "van-dialog"
description: "Dialog component for modal interactions with alerts, confirmations, and custom content. Invoke when user needs to implement modal dialogs, confirmation boxes, or alert messages."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Dialog Component

A modal dialog component for message prompts, confirmations, or specific interactive operations. Supports both component and function call methods.

## When to Invoke

Invoke this skill when:
- User needs to show alert messages to users
- User wants to implement confirmation dialogs
- User needs to display modal content with custom components
- User asks about async close operations
- User wants to implement form dialogs or custom modal content

## Features

- **Function Call**: Quick invocation via `showDialog` and `showConfirmDialog`
- **Component Call**: Full customization via component usage
- **Round Button Theme**: Alternative rounded button style
- **Async Close**: Support async operations before closing
- **Custom Content**: Embed any content via slots
- **Keyboard Support**: Enter/Esc key bindings
- **Teleport**: Mount to specified element

## API Reference

### Methods

| Name | Description | Arguments | Return Value |
|------|-------------|-----------|--------------|
| showDialog | Display alert dialog with confirm button | `options: DialogOptions` | `Promise<void>` |
| showConfirmDialog | Display confirmation dialog | `options: DialogOptions` | `Promise<void>` |
| closeDialog | Close the currently displayed dialog | - | `void` |
| setDialogDefaultOptions | Modify default configuration | `options: DialogOptions` | `void` |
| resetDialogDefaultOptions | Reset default configuration | - | `void` |

### DialogOptions

| Name | Description | Type | Default |
|------|-------------|------|---------|
| title | Title | `string` | - |
| width | Dialog width | `number \| string` | `320px` |
| message | Message | `string \| () => JSX.Element` | - |
| messageAlign | Message text align | `string` | `center` |
| theme | Theme style, can be `round-button` | `string` | `default` |
| className | Custom className | `string \| Array \| object` | - |
| showConfirmButton | Whether to show confirm button | `boolean` | `true` |
| showCancelButton | Whether to show cancel button | `boolean` | `false` |
| cancelButtonText | Cancel button text | `string` | `Cancel` |
| cancelButtonColor | Cancel button color | `string` | `black` |
| cancelButtonDisabled | Whether to disable cancel button | `boolean` | `false` |
| confirmButtonText | Confirm button text | `string` | `Confirm` |
| confirmButtonColor | Confirm button color | `string` | `#ee0a24` |
| confirmButtonDisabled | Whether to disable confirm button | `boolean` | `false` |
| destroyOnClose | Whether to destroy content when closed | `boolean` | `false` |
| overlay | Whether to show overlay | `boolean` | `true` |
| overlayClass | Custom overlay class | `string \| Array \| object` | - |
| overlayStyle | Custom overlay style | `object` | - |
| closeOnPopstate | Whether to close when popstate | `boolean` | `true` |
| closeOnClickOverlay | Whether to close when overlay is clicked | `boolean` | `false` |
| lockScroll | Whether to lock body scroll | `boolean` | `true` |
| allowHtml | Whether to allow HTML rendering | `boolean` | `false` |
| beforeClose | Callback function before close | `(action: string) => boolean \| Promise<boolean>` | - |
| transition | Transition name | `string` | - |
| teleport | Target element for mounting | `string \| Element` | `body` |
| keyboardEnabled | Enable keyboard Enter/Esc | `boolean` | `true` |

### Props (Component Usage)

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model:show | Whether to show dialog | `boolean` | - |
| title | Title | `string` | - |
| width | Width | `number \| string` | `320px` |
| message | Message | `string \| () => JSX.Element` | - |
| message-align | Message align | `string` | `center` |
| theme | Theme style | `string` | `default` |
| show-confirm-button | Whether to show confirm button | `boolean` | `true` |
| show-cancel-button | Whether to show cancel button | `boolean` | `false` |
| cancel-button-text | Cancel button text | `string` | `Cancel` |
| cancel-button-color | Cancel button color | `string` | `black` |
| cancel-button-disabled | Whether to disable cancel button | `boolean` | `false` |
| confirm-button-text | Confirm button text | `string` | `Confirm` |
| confirm-button-color | Confirm button color | `string` | `#ee0a24` |
| confirm-button-disabled | Whether to disable confirm button | `boolean` | `false` |
| z-index | z-index | `number \| string` | `2000+` |
| overlay | Whether to show overlay | `boolean` | `true` |
| close-on-click-overlay | Whether to close when overlay is clicked | `boolean` | `false` |
| lock-scroll | Whether to lock background scroll | `boolean` | `true` |
| before-close | Callback before close | `(action: string) => boolean \| Promise<boolean>` | - |

### Events

| Event | Description | Parameters |
|-------|-------------|------------|
| confirm | Emitted when confirm button is clicked | - |
| cancel | Emitted when cancel button is clicked | - |
| open | Emitted when opening Dialog | - |
| close | Emitted when closing Dialog | - |
| opened | Emitted when Dialog is opened | - |
| closed | Emitted when Dialog is closed | - |

### Slots

| Name | Description |
|------|-------------|
| default | Custom message content |
| title | Custom title |
| footer | Custom footer |

## Usage Examples

### Alert Dialog

```vue
<script setup>
import { showDialog } from 'vant'

const showAlert = () => {
  showDialog({
    title: 'Title',
    message: 'This is an alert message.'
  }).then(() => {
    console.log('Dialog closed')
  })
}
</script>
```

### Confirm Dialog

```vue
<script setup>
import { showConfirmDialog } from 'vant'

const showConfirm = () => {
  showConfirmDialog({
    title: 'Confirm',
    message: 'Are you sure you want to proceed?'
  })
    .then(() => {
      console.log('Confirmed')
    })
    .catch(() => {
      console.log('Cancelled')
    })
}
</script>
```

### Round Button Style

```vue
<script setup>
import { showDialog } from 'vant'

const showRoundDialog = () => {
  showDialog({
    title: 'Title',
    message: 'Round button style dialog',
    theme: 'round-button'
  })
}
</script>
```

### Async Close

```vue
<script setup>
import { showConfirmDialog } from 'vant'

const showAsyncDialog = () => {
  showConfirmDialog({
    title: 'Async Close',
    message: 'Dialog will close after 1 second',
    beforeClose: (action) => {
      return new Promise((resolve) => {
        setTimeout(() => {
          resolve(action === 'confirm')
        }, 1000)
      })
    }
  })
}
</script>
```

### Component Usage

```vue
<template>
  <van-dialog 
    v-model:show="show" 
    title="Title" 
    show-cancel-button
    @confirm="handleConfirm"
  >
    <img src="https://example.com/image.jpg" />
  </van-dialog>
</template>

<script setup>
import { ref } from 'vue'

const show = ref(false)

const handleConfirm = () => {
  console.log('Confirmed')
}
</script>
```

### Custom Footer

```vue
<template>
  <van-dialog v-model:show="show" title="Custom Footer">
    <p>Custom content here</p>
    <template #footer>
      <van-button block @click="show = false">Close</van-button>
    </template>
  </van-dialog>
</template>
```

## Common Issues

### 1. Dialog Not Closing on Overlay Click

By default, `closeOnClickOverlay` is `false`. Enable it if needed:

```js
showDialog({
  message: 'Message',
  closeOnClickOverlay: true
})
```

### 2. HTML Content Not Rendering

Enable `allowHtml` for HTML content:

```js
showDialog({
  message: '<strong>Bold text</strong>',
  allowHtml: true
})
```

### 3. Preventing Dialog Close

Use `beforeClose` to prevent closing:

```js
showConfirmDialog({
  message: 'Message',
  beforeClose: (action) => {
    if (action === 'confirm') {
      return validateForm()
    }
    return true
  }
})
```

## Component Interactions

### With Form Validation

```vue
<script setup>
import { ref } from 'vue'
import { showConfirmDialog, showToast } from 'vant'

const form = ref({ name: '', email: '' })

const submitForm = async () => {
  if (!form.value.name) {
    showToast('Please enter name')
    return
  }
  
  try {
    await showConfirmDialog({
      title: 'Submit',
      message: 'Are you sure to submit?'
    })
    await submitToServer(form.value)
    showToast('Success')
  } catch {
    console.log('Cancelled')
  }
}
</script>
```

### With Loading State

```vue
<script setup>
import { showConfirmDialog, closeDialog } from 'vant'

const saveWithLoading = () => {
  showConfirmDialog({
    title: 'Saving...',
    message: 'Please wait',
    showCancelButton: false,
    closeOnClickOverlay: false,
    beforeClose: async () => {
      await saveData()
      return true
    }
  })
}
</script>
```

## Best Practices

1. **Clear messages**: Keep dialog messages concise and clear
2. **Action labels**: Use descriptive button text (e.g., "Delete" instead of "Confirm")
3. **Destructive actions**: Use confirmation dialogs for destructive operations
4. **Async operations**: Use `beforeClose` for async validation
5. **Accessibility**: Provide meaningful titles for screen readers
6. **Default options**: Use `setDialogDefaultOptions` for consistent styling
