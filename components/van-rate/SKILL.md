---
name: "van-rate"
description: "Rate component for rating things with stars. Invoke when user needs to implement rating systems, star ratings, or custom icon ratings."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Rate Component

Rate component for rating things with customizable icons and styles.

## When to Invoke

Invoke this skill when:
- User needs to implement a star rating system
- User wants to collect user ratings or feedback
- User needs half-star ratings
- User wants to customize rating icons
- User asks about readonly or disabled rating displays

## Features

- **Custom Icons**: Support for custom selected and void icons
- **Half Star**: Allow half-star ratings for precise scoring
- **Custom Count**: Configurable number of rating items
- **Custom Styling**: Customizable size, color, and gutter
- **Clearable**: Allow clearing rating by clicking same value
- **Disabled/Readonly**: Support for disabled and readonly states
- **Touch Support**: Touch gesture for mobile devices
- **Change Events**: Real-time value change notifications

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model | Current rate | `number` | - |
| count | Count | `number \| string` | `5` |
| size | Icon size | `number \| string` | `20px` |
| gutter | Icon gutter | `number \| string` | `4px` |
| color | Selected color | `string` | `#ee0a24` |
| void-color | Void color | `string` | `#c8c9cc` |
| disabled-color | Disabled color | `string` | `#c8c9cc` |
| icon | Selected icon | `string` | `star` |
| void-icon | Void icon | `string` | `star-o` |
| icon-prefix | Icon className prefix | `string` | `van-icon` |
| allow-half | Whether to allow half star | `boolean` | `false` |
| clearable | Whether to allow clear when click again | `boolean` | `false` |
| readonly | Whether to be readonly | `boolean` | `false` |
| disabled | Whether to disable rate | `boolean` | `false` |
| touchable | Whether to allow select rate by touch gesture | `boolean` | `true` |

### Events

| Event | Description | Parameters |
|-------|-------------|------------|
| change | Emitted when rate changed | `currentValue: number` |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-rate v-model="value" />
</template>

<script setup>
import { ref } from 'vue'

const value = ref(3)
</script>
```

### Custom Icon

```vue
<template>
  <van-rate v-model="value" icon="like" void-icon="like-o" />
</template>

<script setup>
import { ref } from 'vue'

const value = ref(3)
</script>
```

### Custom Style

```vue
<template>
  <van-rate
    v-model="value"
    :size="25"
    color="#ffd21e"
    void-icon="star"
    void-color="#eee"
  />
</template>

<script setup>
import { ref } from 'vue'

const value = ref(3)
</script>
```

### Half Star

```vue
<template>
  <van-rate v-model="value" allow-half />
</template>

<script setup>
import { ref } from 'vue'

const value = ref(2.5)
</script>
```

### Custom Count

```vue
<template>
  <van-rate v-model="value" :count="6" />
</template>

<script setup>
import { ref } from 'vue'

const value = ref(3)
</script>
```

### Clearable

```vue
<template>
  <van-rate v-model="value" clearable />
</template>

<script setup>
import { ref } from 'vue'

const value = ref(3)
</script>
```

### Disabled State

```vue
<template>
  <van-rate v-model="value" disabled />
</template>

<script setup>
import { ref } from 'vue'

const value = ref(3)
</script>
```

### Readonly State

```vue
<template>
  <van-rate v-model="value" readonly />
</template>

<script setup>
import { ref } from 'vue'

const value = ref(3)
</script>
```

### Readonly Half Star

```vue
<template>
  <van-rate v-model="value" readonly />
</template>

<script setup>
import { ref } from 'vue'

const value = ref(3.3)
</script>
```

### Change Event

```vue
<template>
  <van-rate v-model="value" @change="onChange" />
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const value = ref(3)

const onChange = (value) => {
  showToast('Current value: ' + value)
}
</script>
```

### With Form

```vue
<template>
  <van-form @submit="onSubmit">
    <van-field name="rate" label="Rating">
      <template #input>
        <van-rate v-model="rate" />
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

const rate = ref(0)

const onSubmit = () => {
  showToast('Rating: ' + rate.value)
}
</script>
```

### Product Rating

```vue
<template>
  <div class="product-rating">
    <div class="rating-header">
      <span class="rating-label">Product Rating</span>
      <span class="rating-value">{{ value }}.0</span>
    </div>
    <van-rate 
      v-model="value" 
      :size="28"
      color="#ffd21e"
      void-color="#eee"
      @change="onRatingChange"
    />
    <div class="rating-text">{{ ratingText }}</div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const value = ref(0)

const ratingText = computed(() => {
  const texts = ['', 'Poor', 'Fair', 'Good', 'Very Good', 'Excellent']
  return texts[value.value] || ''
})

const onRatingChange = (val) => {
  console.log('Rating changed to:', val)
}
</script>

<style scoped>
.product-rating {
  padding: 16px;
}

.rating-header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 8px;
}

.rating-label {
  font-size: 14px;
  color: #323233;
}

.rating-value {
  font-size: 14px;
  color: #ffd21e;
  font-weight: bold;
}

.rating-text {
  margin-top: 8px;
  font-size: 12px;
  color: #969799;
}
</style>
```

## Best Practices

1. **Appropriate Count**: Use 5 stars for standard ratings, adjust based on use case
2. **Half Star**: Enable half-star for precise ratings when needed
3. **Clearable**: Enable clearable to allow users to reset their rating
4. **Readonly Display**: Use readonly for displaying existing ratings
5. **Visual Feedback**: Provide text feedback alongside the rating
6. **Touch Optimization**: Ensure adequate size for touch targets on mobile
7. **Accessibility**: Include labels for screen readers
8. **Color Consistency**: Use colors that match your app's design system
