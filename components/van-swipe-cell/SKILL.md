---
name: "van-swipe-cell"
description: "Swipe cell component for implementing swipe-to-reveal actions. Invoke when user needs to implement swipeable list items, delete/modify actions, or gesture-based cell interactions."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant SwipeCell Component

A cell component that can be swiped left and right to reveal operation buttons.

## When to Invoke

Invoke this skill when:
- User needs to implement swipeable list items
- User wants to reveal action buttons on swipe
- User needs delete or edit actions on swipe
- User asks about implementing swipe gestures
- User wants confirmation before destructive actions

## Features

- **Left/Right Swipe**: Support both directions
- **Custom Width**: Configurable swipe area width
- **Before Close**: Async close confirmation
- **Programmatic Control**: Open/close via methods
- **Disabled State**: Option to disable swiping
- **Custom Content**: Full customization via slots

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| name | Identifier of SwipeCell | `number \| string` | - |
| left-width | Width of left swipe area | `number \| string` | `auto` |
| right-width | Width of right swipe area | `number \| string` | `auto` |
| before-close | Callback before close | `(args) => boolean \| Promise<boolean>` | - |
| disabled | Whether to disable swipe | `boolean` | `false` |
| stop-propagation | Whether to stop touchmove propagation | `boolean` | `false` |

### Slots

| Name | Description |
|------|-------------|
| default | Custom content |
| left | Content of left scrollable area |
| right | Content of right scrollable area |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| click | Emitted when SwipeCell is clicked | `position: 'left' \| 'right' \| 'cell' \| 'outside'` |
| open | Emitted when SwipeCell is opened | `{ name: string \| number, position: 'left' \| 'right' }` |
| close | Emitted when SwipeCell is closed | `{ name: string \| number, position: 'left' \| 'right' \| 'cell' \| 'outside' }` |

### beforeClose Params

| Name | Description | Type |
|------|-------------|------|
| event | The event that triggers closing | `MouseEvent \| TouchEvent` |
| name | Name | `string \| number` |
| position | Click position | `'left' \| 'right' \| 'cell' \| 'outside'` |

### Methods

| Name | Description | Arguments | Return Value |
|------|-------------|-----------|--------------|
| open | Open SwipeCell | `position: 'left' \| 'right'` | - |
| close | Close SwipeCell | - | - |

### Types

```ts
import type {
  SwipeCellSide,
  SwipeCellProps,
  SwipeCellPosition,
  SwipeCellInstance
} from 'vant'
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-swipe-cell>
    <template #left>
      <van-button square type="primary" text="Select" />
    </template>
    <van-cell :border="false" title="Cell" value="Cell Content" />
    <template #right>
      <van-button square type="danger" text="Delete" />
      <van-button square type="primary" text="Collect" />
    </template>
  </van-swipe-cell>
</template>
```

### With Card Component

```vue
<template>
  <van-swipe-cell>
    <van-card
      num="2"
      price="2.00"
      desc="Description"
      title="Title"
      class="goods-card"
      thumb="https://fastly.jsdelivr.net/npm/@vant/assets/cat.jpeg"
    />
    <template #right>
      <van-button square text="Delete" type="danger" class="delete-button" />
    </template>
  </van-swipe-cell>
</template>

<style scoped>
.goods-card {
  margin: 0;
  background-color: #fff;
}

.delete-button {
  height: 100%;
}
</style>
```

### Before Close Confirmation

```vue
<template>
  <van-swipe-cell :before-close="beforeClose">
    <template #left>
      <van-button square type="primary" text="Select" />
    </template>
    <van-cell :border="false" title="Cell" value="Cell Content" />
    <template #right>
      <van-button square type="danger" text="Delete" />
    </template>
  </van-swipe-cell>
</template>

<script setup>
import { showConfirmDialog } from 'vant'

const beforeClose = ({ position }) => {
  switch (position) {
    case 'left':
    case 'cell':
    case 'outside':
      return true
    case 'right':
      return new Promise((resolve) => {
        showConfirmDialog({
          title: 'Are you sure to delete?'
        })
          .then(() => resolve(true))
          .catch(() => resolve(false))
      })
  }
}
</script>
```

### Programmatic Control

```vue
<template>
  <van-swipe-cell ref="swipeCellRef">
    <van-cell title="Cell" />
    <template #right>
      <van-button square type="danger" text="Delete" />
    </template>
  </van-swipe-cell>
  
  <van-button @click="openLeft">Open Left</van-button>
  <van-button @click="closeCell">Close</van-button>
</template>

<script setup>
import { ref } from 'vue'

const swipeCellRef = ref()

const openLeft = () => {
  swipeCellRef.value?.open('left')
}

const closeCell = () => {
  swipeCellRef.value?.close()
}
</script>
```

### Custom Width

```vue
<template>
  <van-swipe-cell :left-width="100" :right-width="150">
    <template #left>
      <van-button square type="primary">Select</van-button>
    </template>
    <van-cell title="Cell" />
    <template #right>
      <van-button square type="primary">Edit</van-button>
      <van-button square type="danger">Delete</van-button>
    </template>
  </van-swipe-cell>
</template>
```

## Common Issues

### 1. Swipe Not Working in List

Ensure no conflicting touch handlers:

```vue
<van-swipe-cell :stop-propagation="true">
  <!-- content -->
</van-swipe-cell>
```

### 2. Button Height Not Matching Cell

Set button height to 100%:

```vue
<template #right>
  <van-button square type="danger" style="height: 100%">Delete</van-button>
</template>
```

### 3. Multiple Cells Open Simultaneously

Track open state and close others:

```vue
<script setup>
const openCellId = ref(null)

const handleOpen = ({ name }) => {
  openCellId.value = name
}

const handleClose = () => {
  openCellId.value = null
}
</script>
```

## Component Interactions

### With List and Delete

```vue
<template>
  <van-list v-model:loading="loading" :finished="finished" @load="onLoad">
    <van-swipe-cell 
      v-for="item in list" 
      :key="item.id"
      :name="item.id"
      :before-close="beforeClose"
    >
      <van-cell :title="item.title" />
      <template #right>
        <van-button square type="danger" text="Delete" @click="deleteItem(item)" />
      </template>
    </van-swipe-cell>
  </van-list>
</template>

<script setup>
import { ref } from 'vue'
import { showConfirmDialog } from 'vant'

const list = ref([])

const deleteItem = async (item) => {
  try {
    await showConfirmDialog({ title: 'Delete this item?' })
    list.value = list.value.filter(i => i.id !== item.id)
  } catch {
    // Cancelled
  }
}
</script>
```

### With Shopping Cart

```vue
<template>
  <van-swipe-cell v-for="item in cartItems" :key="item.id">
    <van-card
      :title="item.name"
      :price="item.price"
      :num="item.quantity"
      :thumb="item.image"
    />
    <template #right>
      <van-button square type="danger" text="Remove" @click="removeFromCart(item)" />
    </template>
  </van-swipe-cell>
</template>
```

### With Edit Actions

```vue
<template>
  <van-swipe-cell>
    <van-cell :title="item.title" :value="item.value" />
    <template #left>
      <van-button square type="primary" @click="editItem(item)">Edit</van-button>
    </template>
    <template #right>
      <van-button square type="danger" @click="deleteItem(item)">Delete</van-button>
    </template>
  </van-swipe-cell>
</template>
```

## Best Practices

1. **Confirmation**: Use `before-close` for destructive actions
2. **Button sizing**: Ensure buttons match cell height
3. **Accessibility**: Provide alternative ways to access actions
4. **Touch targets**: Make buttons large enough for touch
5. **Visual feedback**: Use appropriate colors for action types
6. **Performance**: Avoid heavy operations during swipe
