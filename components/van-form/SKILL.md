---
name: "van-form"
description: "Form component for data entry and verification. Invoke when user needs to implement form validation, submission, or complex form layouts."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Form Component

Used for data entry and verification, supports input boxes, radio buttons, checkboxes, file uploads and other types.

## When to Invoke

Invoke this skill when:
- User needs to implement form submission
- User wants to add form validation
- User needs to handle form errors
- User wants to create complex form layouts
- User asks about form field types (switch, checkbox, radio, etc.)
- User needs to validate specific fields

## Features

- **Form Validation**: Built-in validation with custom rules
- **Multiple Field Types**: Support for various input types
- **Async Validation**: Support for asynchronous validation
- **Error Handling**: Automatic error display and scrolling
- **Form Methods**: Submit, validate, reset validation
- **Custom Triggers**: Configurable validation triggers
- **Auto Required**: Automatic required mark based on rules

## API Reference

### Props

| Attribute | Description | Type | Default |
|-----------|-------------|------|---------|
| label-width | Field label width | `number \| string` | `6.2em` |
| label-align | Field label align, can be set to `center` `right` `top` | `string` | `left` |
| input-align | Field input align, can be set to `center` `right` | `string` | `left` |
| error-message-align | Error message align, can be set to `center` `right` | `string` | `left` |
| validate-trigger | When to validate the form, can be set to `onChange`、`onSubmit`, supports using array to set multiple values | `string \| string[]` | `onBlur` |
| colon | Whether to display colon after label | `boolean` | `false` |
| disabled | Whether to disable form | `boolean` | `false` |
| readonly | Whether to be readonly | `boolean` | `false` |
| required | Whether to show required mark | `boolean \| 'auto'` | `null` |
| validate-first | Whether to stop the validation when a rule fails | `boolean` | `false` |
| scroll-to-error | Whether to scroll to the error field when validation failed | `boolean` | `false` |
| scroll-to-error-position | The position when scrolling to the wrong form item | `string` | - |
| show-error | Whether to highlight input when validation failed | `boolean` | `false` |
| show-error-message | Whether to show error message when validation failed | `boolean` | `true` |
| submit-on-enter | Whether to submit form on enter | `boolean` | `true` |

### Data Structure of Rule

| Key | Description | Type |
|-----|-------------|------|
| required | Whether to be a required field | `boolean` |
| message | Error message, can be a function to dynamically return message content | `string \| (value, rule) => string` |
| validator | Custom validator, can return a Promise to validate dynamically | `(value, rule) => boolean \| string \| Promise` |
| pattern | Regexp pattern, if the regexp cannot match, means that the validation fails | `RegExp` |
| trigger | When to validate the form | `string \| string[]` |
| formatter | Format value before validate | `(value, rule) => any` |
| validateEmpty | Controls whether the `validator` and `pattern` options to verify empty values | `boolean` |

### validate-trigger

| Value | Description |
|-------|-------------|
| onSubmit | Trigger validation after submitting form |
| onBlur | Trigger validation after submitting form or blurring input |
| onChange | Trigger validation after submitting form or changing input value |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| submit | Emitted after submitting the form and validation passed | `values: object` |
| failed | Emitted after submitting the form and validation failed | `errorInfo: { values: object, errors: object[] }` |

### Methods

Use ref to get Form instance and call instance methods.

| Name | Description | Attribute | Return value |
|------|-------------|-----------|--------------|
| submit | Submit form | - | - |
| getValues | Get current form values | - | `Record<string, unknown>` |
| validate | Validate form | `name?: string \| string[]` | `Promise<void>` |
| resetValidation | Reset validation | `name?: string \| string[]` | - |
| getValidationStatus | Get validation status of all fields | - | `Record<string, FieldValidationStatus>` |
| scrollToField | Scroll to field | `name: string, alignToTop: boolean` | - |

### Slots

| Name | Description |
|------|-------------|
| default | Form content |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-form @submit="onSubmit">
    <van-cell-group inset>
      <van-field
        v-model="username"
        name="username"
        label="Username"
        placeholder="Username"
        :rules="[{ required: true, message: 'Username is required' }]"
      />
      <van-field
        v-model="password"
        type="password"
        name="password"
        label="Password"
        placeholder="Password"
        :rules="[{ required: true, message: 'Password is required' }]"
      />
    </van-cell-group>
    <div style="margin: 16px;">
      <van-button round block type="primary" native-type="submit">
        Submit
      </van-button>
    </div>
  </van-form>
</template>

<script setup>
import { ref } from 'vue'

const username = ref('')
const password = ref('')

const onSubmit = (values) => {
  console.log('submit', values)
}
</script>
```

### Validate Rules

```vue
<template>
  <van-form @failed="onFailed">
    <van-cell-group inset>
      <van-field
        v-model="value1"
        name="pattern"
        placeholder="Use pattern"
        :rules="[{ pattern, message: 'Error message' }]"
      />
      <van-field
        v-model="value2"
        name="validator"
        placeholder="Use validator"
        :rules="[{ validator, message: 'Error message' }]"
      />
      <van-field
        v-model="value3"
        name="validatorMessage"
        placeholder="Use validator to return message"
        :rules="[{ validator: validatorMessage }]"
      />
      <van-field
        v-model="value4"
        name="asyncValidator"
        placeholder="Use async validator"
        :rules="[{ validator: asyncValidator, message: 'Error message' }]"
      />
    </van-cell-group>
    <div style="margin: 16px;">
      <van-button round block type="primary" native-type="submit">
        Submit
      </van-button>
    </div>
  </van-form>
</template>

<script setup>
import { ref } from 'vue'
import { closeToast, showLoadingToast } from 'vant'

const value1 = ref('')
const value2 = ref('')
const value3 = ref('abc')
const value4 = ref('')
const pattern = /\d{6}/

const validator = (val) => /1\d{10}/.test(val)

const validatorMessage = (val) => `${val} is invalid`

const asyncValidator = (val) =>
  new Promise((resolve) => {
    showLoadingToast('Validating...')
    setTimeout(() => {
      closeToast()
      resolve(val === '1234')
    }, 1000)
  })

const onFailed = (errorInfo) => {
  console.log('failed', errorInfo)
}
</script>
```

### Field Type - Switch

```vue
<template>
  <van-field name="switch" label="Switch">
    <template #input>
      <van-switch v-model="checked" />
    </template>
  </van-field>
</template>

<script setup>
import { ref } from 'vue'

const checked = ref(false)
</script>
```

### Field Type - Checkbox

```vue
<template>
  <van-field name="checkbox" label="Checkbox">
    <template #input>
      <van-checkbox v-model="checked" shape="square" />
    </template>
  </van-field>
  <van-field name="checkboxGroup" label="CheckboxGroup">
    <template #input>
      <van-checkbox-group v-model="groupChecked" direction="horizontal">
        <van-checkbox name="1" shape="square">Checkbox 1</van-checkbox>
        <van-checkbox name="2" shape="square">Checkbox 2</van-checkbox>
      </van-checkbox-group>
    </template>
  </van-field>
</template>

<script setup>
import { ref } from 'vue'

const checked = ref(false)
const groupChecked = ref([])
</script>
```

### Field Type - Radio

```vue
<template>
  <van-field name="radio" label="Radio">
    <template #input>
      <van-radio-group v-model="checked" direction="horizontal">
        <van-radio name="1">Radio 1</van-radio>
        <van-radio name="2">Radio 2</van-radio>
      </van-radio-group>
    </template>
  </van-field>
</template>

<script setup>
import { ref } from 'vue'

const checked = ref('1')
</script>
```

### Field Type - Stepper

```vue
<template>
  <van-field name="stepper" label="Stepper">
    <template #input>
      <van-stepper v-model="value" />
    </template>
  </van-field>
</template>

<script setup>
import { ref } from 'vue'

const value = ref(1)
</script>
```

### Field Type - Rate

```vue
<template>
  <van-field name="rate" label="Rate">
    <template #input>
      <van-rate v-model="value" />
    </template>
  </van-field>
</template>

<script setup>
import { ref } from 'vue'

const value = ref(3)
</script>
```

### Field Type - Slider

```vue
<template>
  <van-field name="slider" label="Slider">
    <template #input>
      <van-slider v-model="value" />
    </template>
  </van-field>
</template>

<script setup>
import { ref } from 'vue'

const value = ref(50)
</script>
```

### Field Type - Uploader

```vue
<template>
  <van-field name="uploader" label="Uploader">
    <template #input>
      <van-uploader v-model="value" />
    </template>
  </van-field>
</template>

<script setup>
import { ref } from 'vue'

const value = ref([
  { url: 'https://fastly.jsdelivr.net/npm/@vant/assets/leaf.jpeg' },
])
</script>
```

### Field Type - Picker

```vue
<template>
  <van-field
    v-model="result"
    is-link
    readonly
    name="picker"
    label="Picker"
    placeholder="Select city"
    @click="showPicker = true"
  />
  <van-popup v-model:show="showPicker" destroy-on-close position="bottom">
    <van-picker
      :model-value="pickerValue"
      :columns="columns"
      @confirm="onConfirm"
      @cancel="showPicker = false"
    />
  </van-popup>
</template>

<script setup>
import { ref } from 'vue'

const result = ref('')
const pickerValue = ref([])
const showPicker = ref(false)
const columns = [
  { text: 'Delaware', value: 'Delaware' },
  { text: 'Florida', value: 'Florida' },
  { text: 'Georgia', value: 'Georgia' },
]

const onConfirm = ({ selectedValues, selectedOptions }) => {
  result.value = selectedOptions[0]?.text
  pickerValue.value = selectedValues
  showPicker.value = false
}
</script>
```

### Field Type - DatePicker

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

### Field Type - Calendar

```vue
<template>
  <van-field
    v-model="result"
    is-link
    readonly
    name="calendar"
    label="Calendar"
    placeholder="Select date"
    @click="showCalendar = true"
  />
  <van-calendar v-model:show="showCalendar" @confirm="onConfirm" />
</template>

<script setup>
import { ref } from 'vue'

const result = ref('')
const showCalendar = ref(false)

const onConfirm = (date) => {
  result.value = `${date.getMonth() + 1}/${date.getDate()}`
  showCalendar.value = false
}
</script>
```

## Best Practices

1. **Validation Rules**: Define clear validation rules for each field to improve user experience.

2. **Async Validation**: Use async validators for server-side validation, show loading indicator during validation.

3. **Error Messages**: Provide clear and helpful error messages for validation failures.

4. **Validation Triggers**: Choose appropriate validation triggers (onChange, onBlur, onSubmit) based on your needs.

5. **Scroll to Error**: Enable `scroll-to-error` to automatically scroll to the first error field.

6. **Custom Field Types**: Use the `input` slot to create custom field types like switch, checkbox, etc.

7. **Form Methods**: Use form methods (validate, resetValidation) for programmatic control.

8. **Auto Required**: Set `required="auto"` on Form to automatically show required marks based on validation rules.
