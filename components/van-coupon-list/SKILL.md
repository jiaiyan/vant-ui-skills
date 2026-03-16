---
name: "van-coupon-list"
description: "Coupon list component for displaying, selecting, and exchanging coupons. Invoke when user needs to implement coupon selection or management functionality."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Coupon Component

Used for redemption and selection of coupons, including CouponCell and CouponList components.

## When to Invoke

Invoke this skill when:
- User needs to display coupon information
- User wants to implement coupon selection
- User needs coupon exchange functionality
- User wants to show available and unavailable coupons
- User asks about coupon list with tabs
- User needs to integrate coupons in checkout flow

## Features

- **Coupon Display**: Show coupon details with value and conditions
- **Coupon Selection**: Single or multiple coupon selection support
- **Coupon Exchange**: Input and exchange coupon codes
- **Available/Unavailable Tabs**: Separate tabs for usable and unusable coupons
- **Loading States**: Loading indicator for exchange operation
- **Custom Styling**: Customizable currency and placeholder images

## API Reference

### CouponCell Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| title | Cell title | `string` | `Coupon` |
| chosen-coupon | Index of chosen coupon | `number \| number[]` | `-1` |
| coupons | Coupon list | `Coupon[]` | `[]` |
| editable | Whether cell is editable | `boolean` | `true` |
| border | Whether to show inner border | `boolean` | `true` |
| currency | Currency symbol | `string` | `¥` |

### CouponList Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model | Current exchange code | `string` | - |
| chosen-coupon | Index of chosen coupon, supports multiple selection (array type) | `number \| number[]` | `-1` |
| coupons | Available coupon list | `CouponInfo[]` | `[]` |
| disabled-coupons | Unavailable coupon list | `CouponInfo[]` | `[]` |
| enabled-title | Title for available coupons | `string` | `Available` |
| disabled-title | Title for unavailable coupons | `string` | `Unavailable` |
| exchange-button-text | Text for exchange button | `string` | `Exchange` |
| exchange-button-loading | Whether to show loading on exchange button | `boolean` | `false` |
| exchange-button-disabled | Whether to disable exchange button | `boolean` | `false` |
| exchange-min-length | Minimum length to enable exchange button | `number` | `1` |
| displayed-coupon-index | Index of displayed coupon | `number` | - |
| close-button-text | Text for close button | `string` | `Close` |
| input-placeholder | Placeholder for input field | `string` | `Coupon code` |
| currency | Currency symbol | `string` | `¥` |
| empty-image | Placeholder image when list is empty | `string` | - |
| show-count | Whether to show coupon count in tab title | `boolean` | `true` |

### CouponList Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| change | Emitted when chosen coupon changes | `index: number` |
| exchange | Emitted when exchanging coupon | `code: string` |

### CouponList Slots

| Name | Description |
|------|-------------|
| list-footer | Content below available coupon list |
| disabled-list-footer | Content below unavailable coupon list |
| list-button | Customize the bottom button |

### CouponInfo Data Structure

| Key | Description | Type |
|-----|-------------|------|
| id | Coupon ID | `string` |
| name | Coupon name | `string` |
| condition | Usage condition | `string` |
| startAt | Start time (timestamp in seconds) | `number` |
| endAt | End time (timestamp in seconds) | `number` |
| description | Coupon description | `string` |
| reason | Reason for being unavailable | `string` |
| value | Coupon value (in cents) | `number` |
| valueDesc | Value text | `string` |
| unitDesc | Unit text | `string` |

### Types

```ts
import type { CouponCellProps, CouponListProps, CouponInfo } from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-coupon-cell
    :coupons="coupons"
    :chosen-coupon="chosenCoupon"
    @click="showList = true"
  />
  
  <van-popup
    v-model:show="showList"
    round
    position="bottom"
    style="height: 90%; padding-top: 4px;"
  >
    <van-coupon-list
      :coupons="coupons"
      :chosen-coupon="chosenCoupon"
      :disabled-coupons="disabledCoupons"
      @change="onChange"
      @exchange="onExchange"
    />
  </van-popup>
</template>

<script setup>
import { ref } from 'vue';

const coupon = {
  available: 1,
  originCondition: 0,
  reason: '',
  value: 150,
  name: 'Coupon name',
  startAt: 1489104000,
  endAt: 1514592000,
  valueDesc: '1.5',
  unitDesc: '元',
};

const coupons = ref([coupon]);
const showList = ref(false);
const chosenCoupon = ref(-1);
const disabledCoupons = ref([coupon]);

const onChange = (index) => {
  showList.value = false;
  chosenCoupon.value = index;
};

const onExchange = (code) => {
  coupons.value.push(coupon);
};
</script>
```

### Multiple Coupon Selection

```vue
<template>
  <van-coupon-cell
    :coupons="coupons"
    :chosen-coupon="chosenCoupons"
    @click="showList = true"
  />
  
  <van-popup v-model:show="showList" position="bottom" round style="height: 90%">
    <van-coupon-list
      v-model="exchangeCode"
      :coupons="coupons"
      :chosen-coupon="chosenCoupons"
      @change="onChange"
      @exchange="onExchange"
    />
  </van-popup>
</template>

<script setup>
import { ref } from 'vue';

const showList = ref(false);
const exchangeCode = ref('');
const chosenCoupons = ref([]);

const coupons = ref([
  { id: '1', name: 'Coupon 1', value: 100, valueDesc: '1', unitDesc: '元', startAt: 1489104000, endAt: 1514592000 },
  { id: '2', name: 'Coupon 2', value: 200, valueDesc: '2', unitDesc: '元', startAt: 1489104000, endAt: 1514592000 },
]);

const onChange = (index) => {
  const idx = chosenCoupons.value.indexOf(index);
  if (idx > -1) {
    chosenCoupons.value.splice(idx, 1);
  } else {
    chosenCoupons.value.push(index);
  }
};

const onExchange = (code) => {
  console.log('Exchange code:', code);
};
</script>
```

### With Exchange Loading

```vue
<template>
  <van-popup v-model:show="showList" position="bottom" round style="height: 90%">
    <van-coupon-list
      v-model="exchangeCode"
      :coupons="coupons"
      :chosen-coupon="chosenCoupon"
      :exchange-button-loading="loading"
      @change="onChange"
      @exchange="onExchange"
    />
  </van-popup>
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const showList = ref(true);
const exchangeCode = ref('');
const chosenCoupon = ref(-1);
const loading = ref(false);

const coupons = ref([]);

const onChange = (index) => {
  chosenCoupon.value = index;
};

const onExchange = async (code) => {
  loading.value = true;
  try {
    await exchangeCoupon(code);
    coupons.value.push({
      id: Date.now().toString(),
      name: 'New Coupon',
      value: 100,
      valueDesc: '1',
      unitDesc: '元',
      startAt: Date.now() / 1000,
      endAt: Date.now() / 1000 + 86400 * 30,
    });
    showToast('Exchange successful');
  } finally {
    loading.value = false;
  }
};
</script>
```

### Custom Currency

```vue
<template>
  <van-coupon-cell
    :coupons="coupons"
    :chosen-coupon="chosenCoupon"
    currency="$"
    @click="showList = true"
  />
  
  <van-popup v-model:show="showList" position="bottom" round style="height: 90%">
    <van-coupon-list
      :coupons="coupons"
      :chosen-coupon="chosenCoupon"
      currency="$"
      @change="onChange"
    />
  </van-popup>
</template>

<script setup>
import { ref } from 'vue';

const showList = ref(false);
const chosenCoupon = ref(-1);
const coupons = ref([
  { id: '1', name: 'Coupon', value: 100, valueDesc: '1', unitDesc: '$', startAt: 1489104000, endAt: 1514592000 },
]);

const onChange = (index) => {
  showList.value = false;
  chosenCoupon.value = index;
};
</script>
```

### With Custom Footer

```vue
<template>
  <van-popup v-model:show="showList" position="bottom" round style="height: 90%">
    <van-coupon-list
      :coupons="coupons"
      :chosen-coupon="chosenCoupon"
      @change="onChange"
    >
      <template #list-footer>
        <div class="coupon-footer">
          More coupons available in the app
        </div>
      </template>
    </van-coupon-list>
  </van-popup>
</template>

<script setup>
import { ref } from 'vue';

const showList = ref(true);
const chosenCoupon = ref(-1);
const coupons = ref([]);

const onChange = (index) => {
  showList.value = false;
  chosenCoupon.value = index;
};
</script>
```

### In Checkout Flow

```vue
<template>
  <div>
    <van-cell-group inset>
      <van-coupon-cell
        :coupons="availableCoupons"
        :chosen-coupon="chosenCouponIndex"
        @click="showCouponList = true"
      />
    </van-cell-group>
    
    <van-submit-bar
      :price="finalPrice"
      button-text="Submit"
      @submit="onSubmit"
    />
    
    <van-popup v-model:show="showCouponList" position="bottom" round style="height: 90%">
      <van-coupon-list
        :coupons="availableCoupons"
        :disabled-coupons="unavailableCoupons"
        :chosen-coupon="chosenCouponIndex"
        @change="onCouponChange"
        @exchange="onExchange"
      />
    </van-popup>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const showCouponList = ref(false);
const chosenCouponIndex = ref(-1);
const originalPrice = ref(10000);

const availableCoupons = ref([
  { id: '1', name: '10元优惠券', value: 1000, valueDesc: '10', unitDesc: '元', condition: '满50元可用', startAt: 1489104000, endAt: 1514592000 },
  { id: '2', name: '20元优惠券', value: 2000, valueDesc: '20', unitDesc: '元', condition: '满100元可用', startAt: 1489104000, endAt: 1514592000 },
]);

const unavailableCoupons = ref([
  { id: '3', name: '已过期优惠券', value: 5000, valueDesc: '50', unitDesc: '元', reason: '已过期', startAt: 1489104000, endAt: 1514592000 },
]);

const finalPrice = computed(() => {
  if (chosenCouponIndex.value >= 0) {
    const coupon = availableCoupons.value[chosenCouponIndex.value];
    return Math.max(0, originalPrice.value - coupon.value);
  }
  return originalPrice.value;
});

const onCouponChange = (index) => {
  showCouponList.value = false;
  chosenCouponIndex.value = index;
};

const onExchange = (code) => {
  console.log('Exchange:', code);
};

const onSubmit = () => {
  console.log('Submit order');
};
</script>
```

## Best Practices

1. **Coupon Data**: Structure coupon data with all required fields
2. **Timestamp Format**: Use Unix timestamp in seconds for startAt/endAt
3. **Value in Cents**: Store coupon value in cents for precision
4. **Loading State**: Show loading indicator during exchange operation
5. **Validation**: Validate exchange code before submission
6. **User Feedback**: Provide clear feedback after coupon selection/exchange
7. **Unavailable Reasons**: Show clear reasons for unavailable coupons
