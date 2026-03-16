---
name: "van-dropdown-menu"
description: "Dropdown menu component for displaying collapsible filter options. Invoke when user needs to implement dropdown filters, sorting options, or collapsible selection menus."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant DropdownMenu Component

A dropdown menu component that displays a list of options sliding down from the top, commonly used for filtering and sorting.

## When to Invoke

Invoke this skill when:
- User needs to implement dropdown filter menus
- User wants to create sorting options
- User needs to display collapsible selection options
- User asks about implementing filter bars
- User wants custom dropdown content

## Features

- **Multiple Items**: Support multiple dropdown items in one menu
- **Custom Content**: Embed custom content in dropdown items
- **Active Color**: Customizable active color
- **Direction Control**: Expand up or down
- **Swipe Threshold**: Horizontal scroll for many items
- **Disabled State**: Support disabling individual items

## API Reference

### DropdownMenu Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| active-color | Active color of title and option | `string` | `#1989fa` |
| direction | Expand direction, can be `up` | `string` | `down` |
| z-index | z-index of menu item | `number \| string` | `10` |
| duration | Transition duration, unit second | `number \| string` | `0.2` |
| overlay | Whether to show overlay | `boolean` | `true` |
| close-on-click-overlay | Whether to close when overlay is clicked | `boolean` | `true` |
| close-on-click-outside | Whether to close when outside is clicked | `boolean` | `true` |
| swipe-threshold | Horizontal scroll threshold | `number \| string` | - |
| auto-locate | Auto-adjust position with transform | `boolean` | `false` |

### DropdownItem Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model | Value of current option | `number \| string` | - |
| title | Item title | `string` | Text of selected option |
| options | Options array | `Option[]` | `[]` |
| disabled | Whether to disable dropdown item | `boolean` | `false` |
| lazy-render | Whether to lazy render until opened | `boolean` | `true` |
| title-class | Title class | `string \| Array \| object` | - |
| teleport | Target element for mounting | `string \| Element` | - |

### Option Data Structure

| Key | Description | Type |
|-----|-------------|------|
| text | Text | `string` |
| value | Value | `number \| string \| boolean` |
| disabled | Whether to disable option | `boolean` |
| icon | Left icon | `string` |

### DropdownMenu Methods

| Name | Description | Arguments | Return Value |
|------|-------------|-----------|--------------|
| close | Close all dropdown items | - | - |

### DropdownItem Methods

| Name | Description | Arguments | Return Value |
|------|-------------|-----------|--------------|
| toggle | Toggle display | `show?: boolean` | - |

### DropdownItem Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| change | Emitted when option is selected | `value: number \| string` |
| open | Emitted when opening menu | - |
| close | Emitted when closing menu | - |
| opened | Emitted when menu is opened | - |
| closed | Emitted when menu is closed | - |

### DropdownItem Slots

| Name | Description |
|------|-------------|
| default | Custom content |
| title | Custom title |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-dropdown-menu>
    <van-dropdown-item v-model="value1" :options="option1" />
    <van-dropdown-item v-model="value2" :options="option2" />
  </van-dropdown-menu>
</template>

<script setup>
import { ref } from 'vue'

const value1 = ref(0)
const value2 = ref('a')
const option1 = [
  { text: 'Option 1', value: 0 },
  { text: 'Option 2', value: 1 },
  { text: 'Option 3', value: 2 }
]
const option2 = [
  { text: 'Option A', value: 'a' },
  { text: 'Option B', value: 'b' },
  { text: 'Option C', value: 'c' }
]
</script>
```

### Custom Content

```vue
<template>
  <van-dropdown-menu ref="menuRef">
    <van-dropdown-item v-model="value" :options="options" />
    <van-dropdown-item title="Filter" ref="itemRef">
      <van-cell center title="Switch 1">
        <template #right-icon>
          <van-switch v-model="switch1" />
        </template>
      </van-cell>
      <van-cell center title="Switch 2">
        <template #right-icon>
          <van-switch v-model="switch2" />
        </template>
      </van-cell>
      <div style="padding: 5px 16px;">
        <van-button type="primary" block round @click="onConfirm">
          Confirm
        </van-button>
      </div>
    </van-dropdown-item>
  </van-dropdown-menu>
</template>

<script setup>
import { ref } from 'vue'

const menuRef = ref()
const itemRef = ref()
const value = ref(0)
const switch1 = ref(false)
const switch2 = ref(false)
const options = [
  { text: 'Option 1', value: 0 },
  { text: 'Option 2', value: 1 }
]

const onConfirm = () => {
  itemRef.value?.toggle()
}
</script>
```

### Custom Active Color

```vue
<template>
  <van-dropdown-menu active-color="#ee0a24">
    <van-dropdown-item v-model="value1" :options="option1" />
    <van-dropdown-item v-model="value2" :options="option2" />
  </van-dropdown-menu>
</template>
```

### Expand Upward

```vue
<template>
  <van-dropdown-menu direction="up">
    <van-dropdown-item v-model="value" :options="options" />
  </van-dropdown-menu>
</template>
```

### Swipe Items

```vue
<template>
  <van-dropdown-menu swipe-threshold="4">
    <van-dropdown-item v-model="v1" :options="options" />
    <van-dropdown-item v-model="v2" :options="options" />
    <van-dropdown-item v-model="v3" :options="options" />
    <van-dropdown-item v-model="v4" :options="options" />
    <van-dropdown-item v-model="v5" :options="options" />
  </van-dropdown-menu>
</template>
```

### Disabled Items

```vue
<template>
  <van-dropdown-menu>
    <van-dropdown-item v-model="value1" disabled :options="option1" />
    <van-dropdown-item v-model="value2" :options="option2" />
  </van-dropdown-menu>
</template>
```

## Common Issues

### 1. Dropdown Position Issues with Transform

Enable `auto-locate` when parent has transform:

```vue
<van-dropdown-menu auto-locate>
  <van-dropdown-item v-model="value" :options="options" />
</van-dropdown-menu>
```

### 2. Closing Dropdown Programmatically

Use ref to close the menu:

```vue
<van-dropdown-menu ref="menuRef">
  <van-dropdown-item v-model="value" :options="options" />
</van-dropdown-menu>

<script setup>
const menuRef = ref()

const closeMenu = () => {
  menuRef.value?.close()
}
</script>
```

### 3. Custom Title Display

Use title slot for custom title:

```vue
<van-dropdown-item v-model="value" :options="options">
  <template #title>
    <van-icon name="filter-o" /> Filter
  </template>
</van-dropdown-item>
```

## Component Interactions

### With List Filtering

```vue
<template>
  <van-dropdown-menu @change="handleFilterChange">
    <van-dropdown-item v-model="sort" :options="sortOptions" />
    <van-dropdown-item v-model="category" :options="categoryOptions" />
  </van-dropdown-menu>
  
  <van-list :finished="finished" @load="onLoad">
    <van-cell v-for="item in list" :key="item.id" :title="item.title" />
  </van-list>
</template>

<script setup>
import { ref, watch } from 'vue'

const sort = ref(0)
const category = ref('all')
const list = ref([])

watch([sort, category], () => {
  list.value = []
  loadList()
})
</script>
```

### With Custom Filter Panel

```vue
<template>
  <van-dropdown-menu>
    <van-dropdown-item title="Price Range">
      <van-slider v-model="priceRange" range :min="0" :max="1000" />
      <van-button type="primary" @click="applyFilter">Apply</van-button>
    </van-dropdown-item>
  </van-dropdown-menu>
</template>
```

## Best Practices

1. **Limit options**: Keep option count reasonable for better UX
2. **Clear labels**: Use descriptive text for options
3. **Default values**: Set sensible default selections
4. **Mobile-friendly**: Consider touch targets for options
5. **Swipe threshold**: Enable horizontal scroll for many items
6. **State persistence**: Remember user selections when appropriate
