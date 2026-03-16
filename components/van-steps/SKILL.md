---
name: "van-steps"
description: "Steps navigation component for displaying progress flow. Invoke when user needs to show step progress, wizard forms, or process tracking."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Steps Component

Used to show the various parts of an action flow and let the user know where the current action fits into the overall flow.

## When to Invoke

Invoke this skill when:
- User needs to display step progress indicators
- User wants to create wizard or multi-step forms
- User needs to show process tracking
- User asks about horizontal or vertical step navigation
- User wants to customize step icons and colors

## Features

- **Horizontal/Vertical Layout**: Support for both directions
- **Custom Icons**: Customizable active, inactive, and finish icons
- **Color Customization**: Custom colors for active and inactive steps
- **Click Events**: Interactive step navigation
- **Custom Slots**: Custom content for each step

## API Reference

### Steps Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| active | Active step index | `number \| string` | `0` |
| direction | Can be set to `vertical` | `string` | `horizontal` |
| active-color | Active step color | `string` | `#1989fa` |
| inactive-color | Inactive step color | `string` | `#969799` |
| active-icon | Active icon name | `string` | `checked` |
| inactive-icon | Inactive icon name | `string` | - |
| finish-icon | Finish icon name | `string` | - |
| icon-prefix | Icon className prefix | `string` | `van-icon` |

### Step Slots

| Name | Description |
|------|-------------|
| default | Step content |
| active-icon | Custom active icon |
| inactive-icon | Custom inactive icon |
| finish-icon | Custom finish icon |

### Steps Events

| Name | Description | Arguments |
|------|-------------|-----------|
| click-step | Emitted when a step's title or icon is clicked | `index: number` |

### Types

```ts
import type { StepsProps, StepsDirection } from 'vant';
```

### CSS Variables

| Name | Default Value | Description |
|------|---------------|-------------|
| --van-step-text-color | `var(--van-text-color-2)` | Text color |
| --van-step-active-color | `var(--van-primary-color)` | Active step color |
| --van-step-process-text-color | `var(--van-text-color)` | Process text color |
| --van-step-font-size | `var(--van-font-size-md)` | Font size |
| --van-step-line-color | `var(--van-border-color)` | Line color |
| --van-step-finish-line-color | `var(--van-primary-color)` | Finish line color |
| --van-step-finish-text-color | `var(--van-text-color)` | Finish text color |
| --van-step-icon-size | `12px` | Icon size |
| --van-step-circle-size | `5px` | Circle size |
| --van-step-circle-color | `var(--van-gray-6)` | Circle color |
| --van-step-horizontal-title-font-size | `var(--van-font-size-sm)` | Horizontal title font size |
| --van-steps-background | `var(--van-background-2)` | Background color |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-steps :active="active">
    <van-step>Step 1</van-step>
    <van-step>Step 2</van-step>
    <van-step>Step 3</van-step>
    <van-step>Step 4</van-step>
  </van-steps>
</template>

<script setup>
import { ref } from 'vue';

const active = ref(1);
</script>
```

### Custom Style

```vue
<template>
  <van-steps :active="active" active-icon="success" active-color="#07c160">
    <van-step>Step 1</van-step>
    <van-step>Step 2</van-step>
    <van-step>Step 3</van-step>
    <van-step>Step 4</van-step>
  </van-steps>
</template>

<script setup>
import { ref } from 'vue';

const active = ref(2);
</script>
```

### Vertical Steps

```vue
<template>
  <van-steps direction="vertical" :active="0">
    <van-step>
      <h3>City A - Status 1</h3>
      <p>2016-07-12 12:40</p>
    </van-step>
    <van-step>
      <h3>City B - Status 2</h3>
      <p>2016-07-11 10:00</p>
    </van-step>
    <van-step>
      <h3>City C - Status 3</h3>
      <p>2016-07-10 09:30</p>
    </van-step>
  </van-steps>
</template>
```

### Clickable Steps

```vue
<template>
  <van-steps :active="active" @click-step="onClickStep">
    <van-step>Step 1</van-step>
    <van-step>Step 2</van-step>
    <van-step>Step 3</van-step>
    <van-step>Step 4</van-step>
  </van-steps>
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const active = ref(0);

const onClickStep = (index) => {
  active.value = index;
  showToast(`Clicked step ${index + 1}`);
};
</script>
```

### Custom Icons

```vue
<template>
  <van-steps :active="active" active-icon="passed" finish-icon="checked">
    <van-step>
      <template #inactive-icon>
        <van-icon name="circle" />
      </template>
      Step 1
    </van-step>
    <van-step>Step 2</van-step>
    <van-step>Step 3</van-step>
  </van-steps>
</template>

<script setup>
import { ref } from 'vue';

const active = ref(1);
</script>
```

### Wizard Form

```vue
<template>
  <div class="wizard-form">
    <van-steps :active="currentStep" active-color="#07c160">
      <van-step>Personal Info</van-step>
      <van-step>Contact</van-step>
      <van-step>Review</van-step>
    </van-steps>

    <div class="step-content">
      <div v-if="currentStep === 0">
        <van-field v-model="form.name" label="Name" placeholder="Enter your name" />
      </div>
      <div v-if="currentStep === 1">
        <van-field v-model="form.email" label="Email" placeholder="Enter your email" />
      </div>
      <div v-if="currentStep === 2">
        <p>Name: {{ form.name }}</p>
        <p>Email: {{ form.email }}</p>
      </div>
    </div>

    <div class="actions">
      <van-button v-if="currentStep > 0" @click="prevStep">Previous</van-button>
      <van-button type="primary" @click="nextStep">
        {{ currentStep === 2 ? 'Submit' : 'Next' }}
      </van-button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const currentStep = ref(0);
const form = ref({
  name: '',
  email: '',
});

const prevStep = () => {
  if (currentStep.value > 0) {
    currentStep.value--;
  }
};

const nextStep = () => {
  if (currentStep.value < 2) {
    currentStep.value++;
  } else {
    // Submit form
    console.log('Form submitted:', form.value);
  }
};
</script>

<style>
.wizard-form {
  padding: 16px;
}

.step-content {
  margin: 20px 0;
  min-height: 200px;
}

.actions {
  display: flex;
  justify-content: space-between;
}
</style>
```

### Order Tracking

```vue
<template>
  <div class="order-tracking">
    <h3>Order Status</h3>
    <van-steps direction="vertical" :active="orderStatus">
      <van-step v-for="(item, index) in trackingSteps" :key="index">
        <h4>{{ item.title }}</h4>
        <p>{{ item.time }}</p>
        <p class="desc">{{ item.description }}</p>
      </van-step>
    </van-steps>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const orderStatus = ref(2);
const trackingSteps = ref([
  { title: 'Order Placed', time: '2024-01-15 10:30', description: 'Your order has been placed' },
  { title: 'Payment Confirmed', time: '2024-01-15 10:35', description: 'Payment received successfully' },
  { title: 'Shipped', time: '2024-01-16 09:00', description: 'Package is on the way' },
  { title: 'Delivered', time: '', description: 'Waiting for delivery' },
]);
</script>

<style>
.order-tracking {
  padding: 16px;
  background: #fff;
}

.desc {
  color: #969799;
  font-size: 12px;
}
</style>
```

## Best Practices

1. **Use appropriate direction**: Use vertical for detailed timelines, horizontal for simple progress
2. **Clear step labels**: Provide clear, concise labels for each step
3. **Interactive navigation**: Use click-step event for navigable steps
4. **Visual feedback**: Use custom icons and colors to match your design
5. **Form integration**: Combine with forms for wizard-style multi-step forms
