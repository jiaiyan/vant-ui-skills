---
name: "van-field"
description: "Field component for user input. Invoke when user needs to implement text input, textarea, or various input types with validation."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Field Component

Field component let users enter and edit text with various input types and validation support.

## When to Invoke

Invoke this skill when:
- User needs to implement text input fields
- User wants to create textarea with auto-resize
- User needs to format input values
- User wants to show error messages
- User asks about form validation
- User needs to implement various input types (tel, number, digit, password)

## Features

- **Multiple Input Types**: text, tel, digit, number, password, textarea
- **Auto Resize**: Textarea auto-resize support
- **Value Formatting**: Format input values
- **Validation**: Form validation rules support
- **Error Display**: Show error messages
- **Icons**: Left and right icon support
- **Clearable**: Clear button support
- **Word Limit**: Show word count limit
- **Custom Slots**: Multiple slots for customization

## API Reference

### Props

| Attribute | Description | Type | Default |
|-----------|-------------|------|---------|
| v-model | Input value | `number \| string` | - |
| label | Left side label | `string` | - |
| name | As the identifier when submitting the form | `string` | - |
| id | Input id, the for attribute of the label also will be set | `string` | `van-field-n-input` |
| type | Input type, support all native types and `digit` type | `FieldType` | `text` |
| size | Size, can be set to `large` `normal` | `string` | - |
| maxlength | Max length of value | `number \| string` | - |
| min | When the input type is `number` or `digit`, set the minimum allowable value | `number` | - |
| max | When the input type is `number` or `digit`, set the maximum allowable value | `number` | - |
| placeholder | Input placeholder | `string` | - |
| border | Whether to show inner border | `boolean` | `true` |
| disabled | Whether to disable field | `boolean` | `false` |
| readonly | Whether to be readonly | `boolean` | `false` |
| colon | Whether to display colon after label | `boolean` | `false` |
| required | Whether to show required mark | `boolean \| 'auto'` | `null` |
| center | Whether to center content vertically | `boolean` | `true` |
| clearable | Whether to be clearable | `boolean` | `false` |
| clear-icon | Clear icon name | `string` | `clear` |
| clear-trigger | When to display the clear icon | `FieldClearTrigger` | `focus` |
| clickable | Whether to show click feedback when clicked | `boolean` | `false` |
| is-link | Whether to show link icon | `boolean` | `false` |
| autofocus | Whether to auto focus, unsupported in iOS | `boolean` | `false` |
| show-word-limit | Whether to show word limit, need to set the `maxlength` prop | `boolean` | `false` |
| error | Whether to mark the input content in red | `boolean` | `false` |
| error-message | Error message | `string` | - |
| error-message-align | Error message align, can be set to `center` `right` | `FieldTextAlign` | `left` |
| formatter | Input value formatter | `(val: string) => string` | - |
| format-trigger | When to format value, can be set to `onBlur` | `FieldFormatTrigger` | `onChange` |
| arrow-direction | Can be set to `left` `up` `down` | `string` | `right` |
| label-class | Label className | `string \| Array \| object` | - |
| label-width | Label width | `number \| string` | `6.2em` |
| label-align | Label align, can be set to `center` `right` `top` | `FieldTextAlign` | `left` |
| input-align | Input align, can be set to `center` `right` | `FieldTextAlign` | `left` |
| autosize | Textarea auto resize, can accept an object | `boolean \| FieldAutosizeConfig` | `false` |
| left-icon | Left side icon name | `string` | - |
| right-icon | Right side icon name | `string` | - |
| icon-prefix | Icon className prefix | `string` | `van-icon` |
| rules | Form validation rules | `FieldRule[]` | - |
| autocomplete | HTML native attribute | `string` | - |
| autocapitalize | HTML native attribute | `string` | - |
| enterkeyhint | HTML native attribute | `FieldEnterKeyHint` | - |
| spellcheck | HTML native attribute | `boolean` | - |
| autocorrect | HTML native attribute, Safari only | `string` | - |
| inputmode | HTML native attribute | `string` | Set automatically according to the `type` prop |
| rows | HTML native attribute, the number of visible text lines for the control, only valid for textarea | `number \| string` | - |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| update:model-value | Emitted when input value changed | `value: string` |
| focus | Emitted when input is focused | `event: Event` |
| blur | Emitted when input is blurred | `event: Event` |
| clear | Emitted when the clear icon is clicked | `event: MouseEvent` |
| click | Emitted when component is clicked | `event: MouseEvent` |
| click-input | Emitted when the input is clicked | `event: MouseEvent` |
| click-left-icon | Emitted when the left icon is clicked | `event: MouseEvent` |
| click-right-icon | Emitted when the right icon is clicked | `event: MouseEvent` |
| start-validate | Emitted when start validation | - |
| end-validate | Emitted when end validation | `{ status: string, message: string }` |

### Methods

Use ref to get Field instance and call instance methods.

| Name | Description | Attribute | Return value |
|------|-------------|-----------|--------------|
| focus | Trigger input focus | - | - |
| blur | Trigger input blur | - | - |

### Slots

| Name | Description | SlotProps |
|------|-------------|-----------|
| label | Custom label | - |
| input | Custom input | - |
| left-icon | Custom left icon | - |
| right-icon | Custom right icon | - |
| button | Insert button | - |
| error-message | Custom error message | `{ message: string }` |
| extra | Custom content on the right | - |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-cell-group inset>
    <van-field v-model="value" label="Label" placeholder="Text" />
  </van-cell-group>
</template>

<script setup>
import { ref } from 'vue'

const value = ref('')
</script>
```

### Custom Type

```vue
<template>
  <van-cell-group inset>
    <van-field v-model="text" label="Text" />
    <van-field v-model="tel" type="tel" label="Phone" />
    <van-field v-model="digit" type="digit" label="Digit" />
    <van-field v-model="number" type="number" label="Number" />
    <van-field v-model="password" type="password" label="Password" />
  </van-cell-group>
</template>

<script setup>
import { ref } from 'vue'

const tel = ref('')
const text = ref('')
const digit = ref('')
const number = ref('')
const password = ref('')
</script>
```

### Disabled

```vue
<template>
  <van-cell-group inset>
    <van-field label="Text" model-value="Input Readonly" readonly />
    <van-field label="Text" model-value="Input Disabled" disabled />
  </van-cell-group>
</template>
```

### Show Icon

```vue
<template>
  <van-cell-group inset>
    <van-field
      v-model="value1"
      label="Text"
      left-icon="smile-o"
      right-icon="warning-o"
      placeholder="Show Icon"
    />
    <van-field
      v-model="value2"
      clearable
      label="Text"
      left-icon="music-o"
      placeholder="Show Clear Icon"
    />
  </van-cell-group>
</template>

<script setup>
import { ref } from 'vue'

const value1 = ref('')
const value2 = ref('123')
</script>
```

### Required

```vue
<template>
  <van-cell-group inset>
    <van-field
      v-model="username"
      required
      label="Username"
      placeholder="Username"
    />
    <van-field v-model="phone" required label="Phone" placeholder="Phone" />
  </van-cell-group>
</template>

<script setup>
import { ref } from 'vue'

const username = ref('')
const phone = ref('')
</script>
```

### Error Info

```vue
<template>
  <van-cell-group inset>
    <van-field v-model="username" error label="Username" placeholder="Username" />
    <van-field
      v-model="phone"
      label="Phone"
      placeholder="Phone"
      error-message="Invalid phone"
    />
  </van-cell-group>
</template>

<script setup>
import { ref } from 'vue'

const username = ref('')
const phone = ref('')
</script>
```

### Insert Button

```vue
<template>
  <van-cell-group inset>
    <van-field v-model="sms" center clearable label="SMS" placeholder="SMS">
      <template #button>
        <van-button size="small" type="primary">Send SMS</van-button>
      </template>
    </van-field>
  </van-cell-group>
</template>

<script setup>
import { ref } from 'vue'

const sms = ref('')
</script>
```

### Format Value

```vue
<template>
  <van-cell-group inset>
    <van-field
      v-model="value1"
      label="Text"
      :formatter="formatter"
      placeholder="Format On Change"
    />
    <van-field
      v-model="value2"
      label="Text"
      :formatter="formatter"
      format-trigger="onBlur"
      placeholder="Format On Blur"
    />
  </van-cell-group>
</template>

<script setup>
import { ref } from 'vue'

const value1 = ref('')
const value2 = ref('')

const formatter = (value) => value.replace(/\d/g, '')
</script>
```

### Auto Resize

```vue
<template>
  <van-cell-group inset>
    <van-field
      v-model="message"
      label="Message"
      type="textarea"
      placeholder="Message"
      rows="1"
      autosize
    />
  </van-cell-group>
</template>

<script setup>
import { ref } from 'vue'

const message = ref('')
</script>
```

### Show Word Limit

```vue
<template>
  <van-cell-group inset>
    <van-field
      v-model="message"
      rows="2"
      autosize
      label="Message"
      type="textarea"
      maxlength="50"
      placeholder="Message"
      show-word-limit
    />
  </van-cell-group>
</template>

<script setup>
import { ref } from 'vue'

const message = ref('')
</script>
```

### Input Align

```vue
<template>
  <van-cell-group inset>
    <van-field
      v-model="value"
      label="Text"
      placeholder="Input Align Right"
      input-align="right"
    />
  </van-cell-group>
</template>

<script setup>
import { ref } from 'vue'

const value = ref('')
</script>
```

### Label Align

```vue
<template>
  <van-cell-group inset>
    <van-field
      v-model="value"
      label="Label"
      placeholder="Align Top"
      label-align="top"
    />
    <van-field
      v-model="value2"
      label="Label"
      placeholder="Align Left"
      label-align="left"
    />
    <van-field
      v-model="value3"
      label="Label"
      placeholder="Align Center"
      label-align="center"
    />
    <van-field
      v-model="value4"
      label="Label"
      placeholder="Align Right"
      label-align="right"
    />
  </van-cell-group>
</template>

<script setup>
import { ref } from 'vue'

const value = ref('')
const value2 = ref('')
const value3 = ref('')
const value4 = ref('')
</script>
```

## Best Practices

1. **Use with Form**: Combine with Form component for validation support.

2. **Input Types**: Use appropriate input types (tel, digit, number) for better mobile keyboard experience.

3. **Auto Resize**: Use `autosize` for textarea to improve user experience.

4. **Validation**: Define validation rules in the `rules` prop for form validation.

5. **Formatting**: Use `formatter` to sanitize or format user input.

6. **Accessibility**: Provide clear labels and placeholders for better accessibility.

7. **Error Handling**: Use `error-message` to provide clear feedback for validation errors.

8. **Word Limit**: Use `show-word-limit` with `maxlength` for text length constraints.
