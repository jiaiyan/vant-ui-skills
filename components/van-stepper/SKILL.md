---
name: "van-stepper"
description: "Stepper component for numeric input with increment and decrement buttons. Invoke when user needs to implement quantity selectors, number inputs, or counter controls."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Stepper Component

Stepper component for numeric input with increment and decrement buttons.

## When to Invoke

Invoke this skill when:
- User needs to implement quantity selectors
- User wants to create number input with controls
- User needs to limit numeric input range
- User wants to implement decimal or integer-only inputs
- User asks about stepper with validation or async control

## Features

- **Range Control**: Configurable min and max values
- **Step Size**: Adjustable increment/decrement steps
- **Decimal Support**: Control decimal precision
- **Integer Mode**: Restrict to integer-only input
- **Custom Size**: Customizable button and input sizes
- **Round Theme**: Alternative rounded button style
- **Long Press**: Long press for rapid increment/decrement
- **Before Change**: Async validation before value change
- **Disabled States**: Disable specific buttons or entire component

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model | Current value | `number \| string` | - |
| min | Min value | `number \| string` | `1` |
| max | Max value | `number \| string` | - |
| auto-fixed | Whether to auto fix value that is out of range | `boolean` | `true` |
| default-value | Default value, valid when v-model is empty | `number \| string` | `1` |
| step | Value change step | `number \| string` | `1` |
| name | Stepper name | `number \| string` | - |
| input-width | Input width | `number \| string` | `32px` |
| button-size | Button size | `number \| string` | `28px` |
| decimal-length | Decimal length | `number \| string` | - |
| theme | Theme, can be set to `round` | `string` | - |
| placeholder | Input placeholder | `string` | - |
| integer | Whether to allow only integers | `boolean` | `false` |
| disabled | Whether to disable value change | `boolean` | `false` |
| disable-plus | Whether to disable plus button | `boolean` | `false` |
| disable-minus | Whether to disable minus button | `boolean` | `false` |
| disable-input | Whether to disable input | `boolean` | `false` |
| before-change | Callback function before changing | `(value: number \| string) => boolean \| Promise<boolean>` | - |
| show-plus | Whether to show plus button | `boolean` | `true` |
| show-minus | Whether to show minus button | `boolean` | `true` |
| show-input | Whether to show input | `boolean` | `true` |
| long-press | Whether to enable the long press gesture | `boolean` | `true` |
| allow-empty | Whether to allow the input value to be empty | `boolean` | `false` |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| change | Emitted when value changed | `value: string, detail: { name: string }` |
| overlimit | Emitted when a disabled button is clicked | - |
| plus | Emitted when the plus button is clicked | - |
| minus | Emitted when the minus button is clicked | - |
| focus | Emitted when the input is focused | `event: Event` |
| blur | Emitted when the input is blurred | `event: Event` |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-stepper v-model="value" />
</template>

<script setup>
import { ref } from 'vue'

const value = ref(1)
</script>
```

### Step Size

```vue
<template>
  <van-stepper v-model="value" step="2" />
</template>

<script setup>
import { ref } from 'vue'

const value = ref(1)
</script>
```

### Range

```vue
<template>
  <van-stepper v-model="value" min="5" max="8" />
</template>

<script setup>
import { ref } from 'vue'

const value = ref(5)
</script>
```

### Integer Only

```vue
<template>
  <van-stepper v-model="value" integer />
</template>

<script setup>
import { ref } from 'vue'

const value = ref(1)
</script>
```

### Disabled State

```vue
<template>
  <van-stepper v-model="value" disabled />
</template>

<script setup>
import { ref } from 'vue'

const value = ref(1)
</script>
```

### Disable Input

```vue
<template>
  <van-stepper v-model="value" disable-input />
</template>

<script setup>
import { ref } from 'vue'

const value = ref(1)
</script>
```

### Decimal Length

```vue
<template>
  <van-stepper v-model="value" step="0.2" :decimal-length="1" />
</template>

<script setup>
import { ref } from 'vue'

const value = ref(1)
</script>
```

### Custom Size

```vue
<template>
  <van-stepper v-model="value" input-width="40px" button-size="32px" />
</template>

<script setup>
import { ref } from 'vue'

const value = ref(1)
</script>
```

### Before Change

```vue
<template>
  <van-stepper v-model="value" :before-change="beforeChange" />
</template>

<script setup>
import { ref } from 'vue'
import { closeToast, showLoadingToast } from 'vant'

const value = ref(1)

const beforeChange = (value) => {
  showLoadingToast({ forbidClick: true })

  return new Promise((resolve) => {
    setTimeout(() => {
      closeToast()
      resolve(true)
    }, 500)
  })
}
</script>
```

### Round Theme

```vue
<template>
  <van-stepper v-model="value" theme="round" button-size="22" disable-input />
</template>

<script setup>
import { ref } from 'vue'

const value = ref(1)
</script>
```

### Shopping Cart Quantity

```vue
<template>
  <div class="cart-item">
    <div class="item-info">
      <van-image :src="product.image" width="80" height="80" />
      <div class="item-details">
        <div class="item-name">{{ product.name }}</div>
        <div class="item-price">${{ product.price }}</div>
      </div>
    </div>
    <van-stepper 
      v-model="product.quantity" 
      min="1" 
      max="99"
      @change="onQuantityChange"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue'

const product = ref({
  id: 1,
  name: 'Product Name',
  price: 99.99,
  quantity: 1,
  image: 'https://fastly.jsdelivr.net/npm/@vant/assets/leaf.jpeg'
})

const onQuantityChange = (value) => {
  console.log('Quantity changed to:', value)
}
</script>

<style scoped>
.cart-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px;
  background: #fff;
}

.item-info {
  display: flex;
  gap: 12px;
}

.item-details {
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.item-name {
  font-size: 14px;
  color: #323233;
  margin-bottom: 8px;
}

.item-price {
  font-size: 16px;
  color: #ee0a24;
  font-weight: bold;
}
</style>
```

### With Form

```vue
<template>
  <van-form @submit="onSubmit">
    <van-field name="stepper" label="Quantity">
      <template #input>
        <van-stepper v-model="quantity" />
      </template>
    </van-field>
    <div style="margin: 16px;">
      <van-button round block type="primary" native-type="submit">
        Submit
      </van-button>
    </div>
  </van-form>
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const quantity = ref(1)

const onSubmit = () => {
  showToast('Quantity: ' + quantity.value)
}
</script>
```

### Async Validation

```vue
<template>
  <van-stepper 
    v-model="value" 
    :before-change="validateStock"
    @overlimit="onOverLimit"
  />
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const value = ref(1)

const validateStock = async (newValue) => {
  const availableStock = 10
  
  if (newValue > availableStock) {
    showToast('Insufficient stock')
    return false
  }
  
  return true
}

const onOverLimit = () => {
  showToast('Reached limit')
}
</script>
```

## Best Practices

1. **Appropriate Range**: Set meaningful min and max values
2. **Step Size**: Use appropriate step sizes for different scenarios
3. **Input Validation**: Use before-change for async validation
4. **User Feedback**: Provide feedback when limits are reached
5. **Decimal Precision**: Set decimal-length for decimal inputs
6. **Long Press**: Enable long-press for quick adjustments
7. **Accessibility**: Ensure buttons have adequate touch targets
8. **Stock Validation**: Validate against available stock in e-commerce
