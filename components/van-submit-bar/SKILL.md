---
name: "van-submit-bar"
description: "Submit bar component for displaying order amount and submitting orders. Invoke when user needs to implement checkout or order submission functionality."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant SubmitBar Component

Used to display the order amount and submit the order with a fixed bottom bar.

## When to Invoke

Invoke this skill when:
- User needs to implement checkout functionality
- User wants to display order total amount
- User needs a fixed bottom submit bar
- User wants to show tips or warnings before submission
- User asks about order submission with loading state
- User needs custom submit button content

## Features

- **Price Display**: Show order total with currency symbol
- **Decimal Precision**: Configurable decimal places for price
- **Submit Button**: Built-in submit button with loading state
- **Tip Messages**: Display tips or warnings above the bar
- **Custom Content**: Flexible slots for custom content
- **Safe Area**: Bottom safe area adaptation for mobile devices
- **Disabled State**: Disable submission when conditions not met

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| price | Price amount (in cents) | `number` | - |
| decimal-length | Number of decimal places for price | `number \| string` | `2` |
| label | Label text before price | `string` | `Total: ` |
| suffix-label | Label text after price | `string` | - |
| text-align | Text alignment for price label | `string` | `right` |
| button-text | Text for submit button | `string` | - |
| button-type | Type for submit button | `string` | `danger` |
| button-color | Color for submit button | `string` | - |
| tip | Tip message | `string` | - |
| tip-icon | Icon for tip message | `string` | - |
| currency | Currency symbol | `string` | `¥` |
| disabled | Whether to disable submit button | `boolean` | `false` |
| loading | Whether to show loading state | `boolean` | `false` |
| safe-area-inset-bottom | Whether to enable bottom safe area | `boolean` | `true` |
| placeholder | Whether to generate placeholder element | `boolean` | `false` |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| submit | Emitted when submit button is clicked | - |

### Slots

| Name | Description |
|------|-------------|
| default | Custom content on the left side |
| button | Custom submit button |
| top | Custom content above the bar |
| tip | Custom tip content |

### Types

```ts
import type { SubmitBarProps, SubmitBarTextAlign } from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-submit-bar :price="3050" button-text="Submit" @submit="onSubmit" />
</template>

<script setup>
import { showToast } from 'vant';

const onSubmit = () => {
  showToast('Submit order');
};
</script>
```

### With Disabled State

```vue
<template>
  <van-submit-bar
    disabled
    :price="3050"
    button-text="Submit"
    tip="Some tips"
    tip-icon="info-o"
    @submit="onSubmit"
  />
</template>

<script setup>
import { showToast } from 'vant';

const onSubmit = () => {
  showToast('Submit order');
};
</script>
```

### With Loading State

```vue
<template>
  <van-submit-bar
    loading
    :price="3050"
    button-text="Submit"
    @submit="onSubmit"
  />
</template>

<script setup>
import { showToast } from 'vant';

const onSubmit = () => {
  showToast('Submit order');
};
</script>
```

### With Custom Content

```vue
<template>
  <van-submit-bar :price="3050" button-text="Submit" @submit="onSubmit">
    <van-checkbox v-model="checked">Agree to terms</van-checkbox>
    <template #tip>
      Some tips, <span @click="onClickLink">view details</span>
    </template>
  </van-submit-bar>
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const checked = ref(false);

const onSubmit = () => {
  showToast('Submit order');
};

const onClickLink = () => {
  showToast('View details');
};
</script>
```

### Shopping Cart Checkout

```vue
<template>
  <div>
    <van-card
      v-for="item in cartItems"
      :key="item.id"
      :title="item.title"
      :price="item.price"
      :num="item.num"
      :thumb="item.thumb"
    />
    
    <van-submit-bar
      :price="totalPrice"
      button-text="Checkout"
      @submit="onSubmit"
    >
      <van-checkbox v-model="selectAll">Select All</van-checkbox>
    </van-submit-bar>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import { showToast } from 'vant';

const selectAll = ref(false);

const cartItems = ref([
  { id: 1, title: 'Product 1', price: '1000', num: 2, thumb: 'https://via.placeholder.com/100' },
  { id: 2, title: 'Product 2', price: '2000', num: 1, thumb: 'https://via.placeholder.com/100' },
]);

const totalPrice = computed(() => {
  return cartItems.value.reduce((sum, item) => sum + Number(item.price) * item.num, 0);
});

const onSubmit = () => {
  showToast('Checkout');
};
</script>
```

### With Custom Button

```vue
<template>
  <van-submit-bar :price="3050" @submit="onSubmit">
    <template #button>
      <van-button type="primary" round>Custom Button</van-button>
    </template>
  </van-submit-bar>
</template>

<script setup>
import { showToast } from 'vant';

const onSubmit = () => {
  showToast('Submit');
};
</script>
```

### With Tip and Warning

```vue
<template>
  <van-submit-bar
    :price="totalPrice"
    :disabled="!canSubmit"
    button-text="Submit Order"
    tip="Please complete shipping information"
    tip-icon="warning-o"
    @submit="onSubmit"
  >
    <template #tip>
      <div v-if="!hasAddress" class="warning">
        <van-icon name="warning-o" /> Please add shipping address
      </div>
    </template>
  </van-submit-bar>
</template>

<script setup>
import { ref, computed } from 'vue';
import { showToast } from 'vant';

const totalPrice = ref(10000);
const hasAddress = ref(false);

const canSubmit = computed(() => hasAddress.value);

const onSubmit = () => {
  showToast('Order submitted');
};
</script>
```

### With Decimal Configuration

```vue
<template>
  <van-submit-bar
    :price="price"
    :decimal-length="3"
    currency="$"
    button-text="Pay Now"
    @submit="onSubmit"
  />
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const price = ref(12345);

const onSubmit = () => {
  showToast('Pay now');
};
</script>
```

### With Top Content

```vue
<template>
  <van-submit-bar :price="3050" button-text="Submit" @submit="onSubmit">
    <template #top>
      <van-cell-group inset>
        <van-cell title="Subtotal" :value="`¥${subtotal}`" />
        <van-cell title="Shipping" :value="`¥${shipping}`" />
        <van-cell title="Discount" :value="`-¥${discount}`" />
      </van-cell-group>
    </template>
  </van-submit-bar>
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const subtotal = ref(100);
const shipping = ref(10);
const discount = ref(5);

const onSubmit = () => {
  showToast('Submit');
};
</script>
```

### With Placeholder

```vue
<template>
  <div>
    <van-submit-bar
      placeholder
      :price="3050"
      button-text="Submit"
      @submit="onSubmit"
    />
  </div>
</template>

<script setup>
import { showToast } from 'vant';

const onSubmit = () => {
  showToast('Submit');
};
</script>
```

### Complete Order Page

```vue
<template>
  <div class="order-page">
    <van-contact-card
      type="edit"
      :name="order.address.name"
      :tel="order.address.tel"
      @click="editAddress"
    />
    
    <van-card
      v-for="item in order.items"
      :key="item.id"
      :title="item.title"
      :price="item.price"
      :num="item.num"
      :thumb="item.thumb"
    />
    
    <van-cell-group inset>
      <van-coupon-cell
        :coupons="coupons"
        :chosen-coupon="chosenCoupon"
        @click="showCoupons = true"
      />
      <van-cell title="Remark" is-link @click="editRemark">
        <template #value>{{ order.remark || 'Add remark' }}</template>
      </van-cell>
    </van-cell-group>
    
    <van-submit-bar
      :price="order.totalPrice"
      :loading="submitting"
      button-text="Submit Order"
      @submit="onSubmit"
    >
      <van-checkbox v-model="agreeTerms">Agree terms</van-checkbox>
      <template #tip>
        <div v-if="!agreeTerms" class="tip">
          Please agree to the terms before submitting
        </div>
      </template>
    </van-submit-bar>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const submitting = ref(false);
const agreeTerms = ref(false);
const chosenCoupon = ref(-1);
const showCoupons = ref(false);

const order = ref({
  address: {
    name: 'John Snow',
    tel: '13000000000',
  },
  items: [
    { id: 1, title: 'Product 1', price: '1000', num: 1, thumb: 'https://via.placeholder.com/100' },
  ],
  totalPrice: 1000,
  remark: '',
});

const coupons = ref([]);

const editAddress = () => {
  showToast('Edit address');
};

const editRemark = () => {
  showToast('Edit remark');
};

const onSubmit = async () => {
  if (!agreeTerms.value) {
    showToast('Please agree to terms');
    return;
  }
  
  submitting.value = true;
  try {
    await submitOrder();
    showToast('Order submitted');
  } finally {
    submitting.value = false;
  }
};

const submitOrder = () => {
  return new Promise(resolve => setTimeout(resolve, 1000));
};
</script>
```

## Best Practices

1. **Price in Cents**: Always pass price in cents for precision
2. **Loading State**: Show loading indicator during async submission
3. **Validation**: Disable submit button when conditions are not met
4. **User Feedback**: Provide clear feedback after submission
5. **Safe Area**: Keep safe-area-inset-bottom enabled for mobile devices
6. **Terms Agreement**: Add checkbox for terms agreement when required
7. **Tip Messages**: Use tip slot for important notices
