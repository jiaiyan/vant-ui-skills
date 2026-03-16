---
name: "van-button"
description: "Button component for mobile interactions with various types, sizes, and styles. Invoke when user needs to implement buttons, loading states, or customize button appearance in mobile applications."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Button Component

Button component for mobile user interactions with multiple types, sizes, and styles.

## When to Invoke

Invoke this skill when:
- User needs to implement a button with specific type or style
- User wants to create loading state buttons
- User needs disabled or plain buttons
- User wants to customize button colors or gradients
- User asks about button icons or shapes
- User needs route navigation buttons
- User wants block-level buttons

## Features

- **Multiple Types**: default, primary, success, warning, danger
- **Multiple Sizes**: large, normal, small, mini
- **Style Variants**: plain, hairline, round, square
- **States**: loading, disabled
- **Custom Colors**: support solid colors and gradients
- **Icon Support**: left or right icon position
- **Route Navigation**: URL links or Vue Router navigation
- **Block Element**: full-width buttons
- **Loading Customization**: custom loading text and icon type

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| type | Button type, can be set to `primary` `success` `warning` `danger` | `string` | `default` |
| size | Button size, can be set to `large` `small` `mini` | `string` | `normal` |
| text | Button text | `string` | - |
| color | Button color, support linear-gradient | `string` | - |
| icon | Left icon name or URL | `string` | - |
| icon-prefix | Icon className prefix | `string` | `van-icon` |
| icon-position | Icon position, can be set to `right` | `string` | `left` |
| tag | HTML tag | `string` | `button` |
| native-type | Native type attribute | `string` | `button` |
| plain | Whether to be plain button | `boolean` | `false` |
| block | Whether to set display block | `boolean` | `false` |
| round | Whether to be round button | `boolean` | `false` |
| square | Whether to be square button | `boolean` | `false` |
| disabled | Whether to disable button | `boolean` | `false` |
| loading | Whether to show loading status | `boolean` | `false` |
| loading-text | Loading text | `string` | - |
| loading-type | Loading type, can be set to `spinner` | `string` | `circular` |
| loading-size | Loading icon size | `number \| string` | `20px` |
| url | Link URL | `string` | - |
| to | Target route for Vue Router navigation | `string \| object` | - |
| replace | If true, navigation will not leave a history record | `boolean` | `false` |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| click | Emitted when button is clicked and not disabled or loading | `event: MouseEvent` |
| touchstart | Emitted when button is touched | `event: TouchEvent` |

### Slots

| Name | Description |
|------|-------------|
| default | Default slot for button content |
| icon | Custom icon slot |
| loading | Custom loading icon slot |

### Types

```ts
import type {
  ButtonType,
  ButtonSize,
  ButtonProps,
  ButtonNativeType,
  ButtonIconPosition,
} from 'vant';
```

## Usage Examples

### Basic Button Types

```vue
<template>
  <div class="button-demo">
    <van-button type="primary">Primary</van-button>
    <van-button type="success">Success</van-button>
    <van-button type="default">Default</van-button>
    <van-button type="danger">Danger</van-button>
    <van-button type="warning">Warning</van-button>
  </div>
</template>
```

### Plain Buttons

```vue
<template>
  <div class="button-demo">
    <van-button plain type="primary">Plain Primary</van-button>
    <van-button plain type="success">Plain Success</van-button>
  </div>
</template>
```

### Hairline Buttons

```vue
<template>
  <div class="button-demo">
    <van-button plain hairline type="primary">Hairline Primary</van-button>
    <van-button plain hairline type="success">Hairline Success</van-button>
  </div>
</template>
```

### Disabled State

```vue
<template>
  <div class="button-demo">
    <van-button disabled type="primary">Disabled Primary</van-button>
    <van-button disabled type="success">Disabled Success</van-button>
  </div>
</template>
```

### Loading State

```vue
<template>
  <div class="button-demo">
    <van-button loading type="primary" />
    <van-button loading type="primary" loading-type="spinner" />
    <van-button loading type="success" loading-text="Loading...">
      Loading
    </van-button>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const loading = ref(false)

const handleClick = () => {
  loading.value = true
  setTimeout(() => {
    loading.value = false
  }, 2000)
}
</script>
```

### Button Shapes

```vue
<template>
  <div class="button-demo">
    <van-button square type="primary">Square</van-button>
    <van-button round type="success">Round</van-button>
  </div>
</template>
```

### Button with Icon

```vue
<template>
  <div class="button-demo">
    <van-button icon="plus" type="primary" />
    <van-button icon="plus" type="primary">Button</van-button>
    <van-button icon="https://fastly.jsdelivr.net/npm/@vant/assets/user-active.png" type="primary">
      Custom Icon
    </van-button>
  </div>
</template>
```

### Button Sizes

```vue
<template>
  <div class="button-demo">
    <van-button type="primary" size="large">Large</van-button>
    <van-button type="primary" size="normal">Normal</van-button>
    <van-button type="primary" size="small">Small</van-button>
    <van-button type="primary" size="mini">Mini</van-button>
  </div>
</template>
```

### Block Button

```vue
<template>
  <van-button type="primary" block>Block Element</van-button>
</template>
```

### Route Navigation

```vue
<template>
  <div class="button-demo">
    <van-button type="primary" url="https://github.com">URL Link</van-button>
    <van-button type="primary" to="index">Vue Router</van-button>
  </div>
</template>
```

### Custom Color

```vue
<template>
  <div class="button-demo">
    <van-button color="#7232dd">Pure Color</van-button>
    <van-button color="#7232dd" plain>Plain Custom</van-button>
    <van-button color="linear-gradient(to right, #ff6034, #ee0a24)">
      Gradient
    </van-button>
  </div>
</template>
```

### Animated Button

```vue
<template>
  <van-button type="danger" round>
    <van-swipe
      vertical
      class="notice-swipe"
      :autoplay="2000"
      :touchable="false"
      :show-indicators="false"
    >
      <van-swipe-item>Do Task</van-swipe-item>
      <van-swipe-item>Lottery</van-swipe-item>
    </van-swipe>
  </van-button>
</template>

<style scoped>
.notice-swipe {
  height: 40px;
  line-height: 40px;
}
</style>
```

## Common Issues

### 1. Button Width Not Consistent

When using icons or loading states, button width may change. Set a fixed width:

```vue
<van-button type="primary" style="width: 100px">Button</van-button>
```

### 2. Custom Color in Plain Mode

When using custom color with plain mode, the text color will be the custom color:

```vue
<van-button color="#7232dd" plain>Plain Button</van-button>
```

### 3. Loading State Text

Use `loading-text` to show text during loading:

```vue
<van-button loading loading-text="Loading..." type="primary">
  Submit
</van-button>
```

## Component Interactions

### With Form

```vue
<template>
  <van-form @submit="onSubmit">
    <van-field name="username" label="Username" />
    <div style="margin: 16px">
      <van-button round block type="primary" native-type="submit">
        Submit
      </van-button>
    </div>
  </van-form>
</template>

<script setup>
const onSubmit = (values) => {
  console.log('submit', values)
}
</script>
```

### With Dialog

```vue
<template>
  <van-button type="primary" @click="showDialog = true">
    Open Dialog
  </van-button>
  
  <van-dialog v-model:show="showDialog" title="Title" show-cancel-button>
    <p>Dialog content</p>
  </van-dialog>
</template>

<script setup>
import { ref } from 'vue'

const showDialog = ref(false)
</script>
```

### With Async Operation

```vue
<template>
  <van-button 
    type="primary" 
    :loading="submitting" 
    @click="handleSubmit"
  >
    {{ submitting ? 'Submitting...' : 'Submit' }}
  </van-button>
</template>

<script setup>
import { ref } from 'vue'

const submitting = ref(false)

const handleSubmit = async () => {
  submitting.value = true
  try {
    await submitData()
  } finally {
    submitting.value = false
  }
}
</script>
```

## Best Practices

1. **Use semantic types**: Use appropriate type for different actions (primary for main actions, danger for destructive actions)
2. **Provide feedback**: Use loading state for async operations
3. **Mobile optimization**: Use appropriate sizes for touch targets (minimum 44px height)
4. **Block buttons**: Use block buttons for primary actions in mobile layouts
5. **Loading state**: Always provide loading feedback for async operations
6. **Accessibility**: Add aria-label for icon-only buttons
7. **Consistent sizing**: Use consistent sizes within the same context
