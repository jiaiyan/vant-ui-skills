---
name: "van-password-input"
description: "Password input component for secure password entry. Invoke when user needs to implement password input with masked display, often used with number keyboard."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant PasswordInput Component

The PasswordInput component is usually used with NumberKeyboard Component for secure password entry.

## When to Invoke

Invoke this skill when:
- User needs to implement password input
- User wants to create verification code input
- User needs masked password display
- User wants to show error messages for passwords
- User asks about password input with custom length

## Features

- **Masked Display**: Hide password characters with dots
- **Custom Length**: Configurable password length
- **Error Display**: Show error messages
- **Info Display**: Show helpful tips
- **Focus State**: Visual focus indicator
- **Custom Gutter**: Adjustable spacing between characters

## API Reference

### Props

| Attribute | Description | Type | Default |
|-----------|-------------|------|---------|
| value | Password value | `string` | `''` |
| info | Bottom info | `string` | - |
| error-info | Bottom error info | `string` | - |
| length | Maxlength of password | `number \| string` | `6` |
| gutter | Gutter of input | `number \| string` | `0` |
| mask | Whether to mask value | `boolean` | `true` |
| focused | Whether to show focused cursor | `boolean` | `false` |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| focus | Emitted when input is focused | - |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-password-input
    :value="value"
    :focused="showKeyboard"
    @focus="showKeyboard = true"
  />
  <van-number-keyboard
    v-model="value"
    :show="showKeyboard"
    @blur="showKeyboard = false"
  />
</template>

<script setup>
import { ref } from 'vue'

const value = ref('123')
const showKeyboard = ref(true)
</script>
```

### Custom Length

```vue
<template>
  <van-password-input
    :value="value"
    :length="4"
    :focused="showKeyboard"
    @focus="showKeyboard = true"
  />
  <van-number-keyboard
    v-model="value"
    :show="showKeyboard"
    @blur="showKeyboard = false"
  />
</template>

<script setup>
import { ref } from 'vue'

const value = ref('')
const showKeyboard = ref(true)
</script>
```

### Add Gutter

```vue
<template>
  <van-password-input
    :value="value"
    :gutter="10"
    :focused="showKeyboard"
    @focus="showKeyboard = true"
  />
  <van-number-keyboard
    v-model="value"
    :show="showKeyboard"
    @blur="showKeyboard = false"
  />
</template>

<script setup>
import { ref } from 'vue'

const value = ref('')
const showKeyboard = ref(true)
</script>
```

### Without Mask

```vue
<template>
  <van-password-input
    :value="value"
    :mask="false"
    :focused="showKeyboard"
    @focus="showKeyboard = true"
  />
  <van-number-keyboard
    v-model="value"
    :show="showKeyboard"
    @blur="showKeyboard = false"
  />
</template>

<script setup>
import { ref } from 'vue'

const value = ref('')
const showKeyboard = ref(true)
</script>
```

### Hint Error

```vue
<template>
  <van-password-input
    :value="value"
    info="Some tips"
    :error-info="errorInfo"
    :focused="showKeyboard"
    @focus="showKeyboard = true"
  />
  <van-number-keyboard
    v-model="value"
    :show="showKeyboard"
    @blur="showKeyboard = false"
  />
</template>

<script setup>
import { ref, watch } from 'vue'

const value = ref('123')
const errorInfo = ref('')
const showKeyboard = ref(true)

watch(value, (newVal) => {
  if (newVal.length === 6 && newVal !== '123456') {
    errorInfo.value = 'Password Mistake'
  } else {
    errorInfo.value = ''
  }
})
</script>
```

## Best Practices

1. **Use with NumberKeyboard**: Always combine with NumberKeyboard for better mobile experience.

2. **Error Handling**: Show clear error messages when password validation fails.

3. **Focus State**: Manage focus state to show cursor and trigger keyboard.

4. **Custom Length**: Adjust length based on your password requirements.

5. **Security**: Keep `mask` enabled for passwords, disable for verification codes if needed.

6. **Info Messages**: Use `info` prop to provide helpful tips to users.

7. **Gutter**: Adjust gutter for better visual separation between characters.
