---
name: "van-number-keyboard"
description: "Number keyboard component for numeric input. Invoke when user needs to implement numeric input with virtual keyboard, often used with password input."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant NumberKeyboard Component

The NumberKeyboard component can be used with PasswordInput component or custom input box components.

## When to Invoke

Invoke this skill when:
- User needs to implement numeric input
- User wants to create a virtual number keyboard
- User needs to input passwords or verification codes
- User wants to customize keyboard layout
- User asks about random key order for security

## Features

- **Two Themes**: Default and custom themes
- **Extra Keys**: Support for extra keys like decimal point
- **Random Order**: Shuffle key order for security
- **Title Support**: Optional keyboard title
- **Custom Slots**: Custom delete and extra key content
- **v-model Binding**: Direct value binding
- **Max Length**: Limit input length
- **Safe Area**: Bottom safe area adaptation

## API Reference

### Props

| Attribute | Description | Type | Default |
|-----------|-------------|------|---------|
| v-model | Current value | `string` | - |
| show | Whether to show keyboard | `boolean` | - |
| title | Keyboard title | `string` | - |
| theme | Keyboard theme, can be set to `custom` | `string` | `default` |
| maxlength | Value maxlength | `number \| string` | `Infinity` |
| transition | Whether to show transition animation | `boolean` | `true` |
| z-index | Keyboard z-index | `number \| string` | `100` |
| extra-key | Content of bottom left key | `string \| string[]` | `''` |
| close-button-text | Close button text | `string` | - |
| delete-button-text | Delete button text | `string` | Delete Icon |
| close-button-loading | Whether to show loading close button in custom theme | `boolean` | `false` |
| show-delete-key | Whether to show delete button | `boolean` | `true` |
| blur-on-close | Whether to emit blur event when clicking close button | `boolean` | `true` |
| hide-on-click-outside | Whether to hide keyboard when outside is clicked | `boolean` | `true` |
| teleport | Specifies a target element where NumberKeyboard will be mounted | `string \| Element` | - |
| safe-area-inset-bottom | Whether to enable bottom safe area adaptation | `boolean` | `true` |
| random-key-order | Whether to shuffle the order of keys | `boolean` | `false` |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| input | Emitted when a key is pressed | `key: string` |
| delete | Emitted when the delete key is pressed | - |
| close | Emitted when the close button is clicked | - |
| blur | Emitted when the close button is clicked or the keyboard is blurred | - |
| show | Emitted when keyboard is fully displayed | - |
| hide | Emitted when keyboard is fully hidden | - |

### Slots

| Name | Description |
|------|-------------|
| delete | Custom delete key content |
| extra-key | Custom extra key content |
| title-left | Custom title left content |

## Usage Examples

### Default Keyboard

```vue
<template>
  <van-cell @touchstart.stop="show = true">Show Keyboard</van-cell>
  <van-number-keyboard
    :show="show"
    @blur="show = false"
    @input="onInput"
    @delete="onDelete"
  />
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const show = ref(true)

const onInput = (value) => showToast(value)
const onDelete = () => showToast('delete')
</script>
```

### Keyboard With Sidebar

```vue
<template>
  <van-number-keyboard
    :show="show"
    theme="custom"
    extra-key="."
    close-button-text="Close"
    @blur="show = false"
    @input="onInput"
    @delete="onDelete"
  />
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const show = ref(true)

const onInput = (value) => showToast(value)
const onDelete = () => showToast('delete')
</script>
```

### IdNumber Keyboard

```vue
<template>
  <van-cell plain type="primary" @touchstart.stop="show = true">
    Show IdNumber Keyboard
  </van-cell>

  <van-number-keyboard
    :show="show"
    extra-key="X"
    close-button-text="Close"
    @blur="show = false"
    @input="onInput"
    @delete="onDelete"
  />
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const show = ref(true)

const onInput = (value) => showToast(value)
const onDelete = () => showToast('delete')
</script>
```

### Keyboard With Title

```vue
<template>
  <van-cell plain type="primary" @touchstart.stop="show = true">
    Show Keyboard With Title
  </van-cell>
  <van-number-keyboard
    :show="show"
    title="Keyboard Title"
    extra-key="."
    close-button-text="Close"
    @blur="show = false"
    @input="onInput"
    @delete="onDelete"
  />
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const show = ref(true)

const onInput = (value) => showToast(value)
const onDelete = () => showToast('delete')
</script>
```

### Multiple ExtraKey

```vue
<template>
  <van-cell plain type="primary" @touchstart.stop="show = true">
    Show Keyboard With Multiple ExtraKey
  </van-cell>
  <van-number-keyboard
    :show="show"
    theme="custom"
    :extra-key="['00', '.']"
    close-button-text="Close"
    @blur="show = false"
    @input="onInput"
    @delete="onDelete"
  />
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const show = ref(true)

const onInput = (value) => showToast(value)
const onDelete = () => showToast('delete')
</script>
```

### Random Key Order

```vue
<template>
  <van-cell @touchstart.stop="show = true">
    Show Keyboard With Random Key Order
  </van-cell>
  <van-number-keyboard
    :show="show"
    random-key-order
    @blur="show = false"
    @input="onInput"
    @delete="onDelete"
  />
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const show = ref(true)

const onInput = (value) => showToast(value)
const onDelete = () => showToast('delete')
</script>
```

### Bind Value

```vue
<template>
  <van-field v-model="value" readonly clickable @touchstart.stop="show = true" />
  <van-number-keyboard
    v-model="value"
    :show="show"
    :maxlength="6"
    @blur="show = false"
  />
</template>

<script setup>
import { ref } from 'vue'

const show = ref(true)
const value = ref('')
</script>
```

## Best Practices

1. **Use with Field**: Combine with Field component for better input experience.

2. **Random Order**: Use `random-key-order` for security-sensitive inputs like passwords.

3. **Max Length**: Set `maxlength` to limit input length for verification codes.

4. **Custom Theme**: Use `theme="custom"` for more flexible layout with sidebar.

5. **Extra Keys**: Use `extra-key` for decimal point or other special characters.

6. **Touch Events**: Use `@touchstart.stop` to prevent default behavior when showing keyboard.

7. **Safe Area**: Enable `safe-area-inset-bottom` for devices with notches.
