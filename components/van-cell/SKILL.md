---
name: "van-cell"
description: "Cell component for displaying items in a list. Invoke when user needs to create list items, settings pages, or navigation menus with icons, links, and custom content."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Cell Component

Cell component for displaying items in a list with flexible content layout.

## When to Invoke

Invoke this skill when:
- User needs to create list items or settings pages
- User wants to display information with title, value, and label
- User needs navigation items with links or router navigation
- User wants to create grouped cells with titles
- User needs cells with icons or custom content
- User asks about cell groups or inset styling
- User wants vertically centered cells

## Features

- **Flexible Layout**: title, value, and label support
- **Cell Groups**: group cells with titles and borders
- **Inset Style**: rounded inset cell groups
- **Icon Support**: left icon and right icon
- **Link Navigation**: URL links or Vue Router navigation
- **Custom Slots**: multiple slots for customization
- **Size Variants**: normal and large sizes
- **Vertical Center**: center content vertically
- **Arrow Direction**: customizable arrow direction

## API Reference

### CellGroup Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| title | Group title | `string` | - |
| inset | Whether to be inset grouped | `boolean` | `false` |
| border | Whether to show outer border | `boolean` | `true` |

### Cell Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| title | Title | `number \| string` | - |
| value | Right text | `number \| string` | - |
| label | Description below the title | `number \| string` | - |
| size | Size, can be set to `large` `normal` | `string` | - |
| icon | Left icon | `string` | - |
| icon-prefix | Icon className prefix | `string` | `van-icon` |
| tag | Custom element tag | `string` | `div` |
| url | Link URL | `string` | - |
| to | Target route for Vue Router navigation | `string \| object` | - |
| replace | If true, navigation will not leave a history record | `boolean` | `false` |
| border | Whether to show inner border | `boolean` | `true` |
| center | Whether to center content vertically | `boolean` | `false` |
| clickable | Whether to show click feedback when clicked | `boolean` | `null` |
| is-link | Whether to show link icon | `boolean` | `false` |
| required | Whether to show required mark | `boolean` | `false` |
| arrow-direction | Arrow direction, can be set to `left` `up` `down` | `string` | `right` |
| title-style | Title style | `string \| Array \| object` | - |
| title-class | Title className | `string \| Array \| object` | - |
| value-class | Value className | `string \| Array \| object` | - |
| label-class | Label className | `string \| Array \| object` | - |

### Cell Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| click | Emitted when cell is clicked | `event: MouseEvent` |

### CellGroup Slots

| Name | Description |
|------|-------------|
| default | Default slot for cell group content |
| title | Custom title slot |

### Cell Slots

| Name | Description |
|------|-------------|
| title | Custom title |
| value | Custom value |
| label | Custom label |
| icon | Custom left icon |
| right-icon | Custom right icon |
| extra | Custom extra content on the right |

### Types

```ts
import type {
  CellSize,
  CellProps,
  CellGroupProps,
  CellArrowDirection,
} from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-cell-group>
    <van-cell title="Cell title" value="Content" />
    <van-cell title="Cell title" value="Content" label="Description" />
  </van-cell-group>
</template>
```

### Inset Grouped

```vue
<template>
  <van-cell-group inset>
    <van-cell title="Cell title" value="Content" />
    <van-cell title="Cell title" value="Content" label="Description" />
  </van-cell-group>
</template>
```

### Large Size

```vue
<template>
  <van-cell-group>
    <van-cell title="Cell title" value="Content" size="large" />
    <van-cell
      title="Cell title"
      value="Content"
      size="large"
      label="Description"
    />
  </van-cell-group>
</template>
```

### Left Icon

```vue
<template>
  <van-cell-group>
    <van-cell title="Cell title" icon="location-o" />
  </van-cell-group>
</template>
```

### Link Navigation

```vue
<template>
  <van-cell-group>
    <van-cell title="Cell title" is-link />
    <van-cell title="Cell title" is-link value="Content" />
    <van-cell title="Cell title" is-link arrow-direction="down" value="Content" />
  </van-cell-group>
</template>
```

### Router Navigation

```vue
<template>
  <van-cell-group>
    <van-cell title="URL" is-link url="https://github.com" />
    <van-cell title="Vue Router" is-link to="index" />
  </van-cell-group>
</template>
```

### Group Title

```vue
<template>
  <van-cell-group title="Group 1">
    <van-cell title="Cell title" value="Content" />
  </van-cell-group>
  <van-cell-group title="Group 2">
    <van-cell title="Cell title" value="Content" />
  </van-cell-group>
</template>
```

### Custom Slots

```vue
<template>
  <van-cell value="Content" is-link>
    <template #title>
      <span class="custom-title">Title</span>
      <van-tag type="primary">Tag</van-tag>
    </template>
  </van-cell>

  <van-cell title="Title" icon="shop-o">
    <template #right-icon>
      <van-icon name="search" class="search-icon" />
    </template>
  </van-cell>
</template>

<style scoped>
.custom-title {
  margin-right: 4px;
  vertical-align: middle;
}

.search-icon {
  font-size: 16px;
  line-height: inherit;
}
</style>
```

### Vertical Center

```vue
<template>
  <van-cell center title="Cell title" value="Content" label="Description" />
</template>
```

### Settings Page Example

```vue
<template>
  <van-cell-group title="Basic Settings">
    <van-cell title="Username" value="Vant" is-link />
    <van-cell title="Avatar" is-link>
      <template #value>
        <van-image
          width="32"
          height="32"
          round
          src="https://fastly.jsdelivr.net/npm/@vant/assets/cat.jpeg"
        />
      </template>
    </van-cell>
    <van-cell title="Gender" value="Male" is-link />
  </van-cell-group>

  <van-cell-group title="Advanced Settings">
    <van-cell title="Privacy" is-link />
    <van-cell title="Notification" is-link />
    <van-cell title="Language" value="English" is-link />
  </van-cell-group>
</template>
```

### With Switch

```vue
<template>
  <van-cell-group title="Notifications">
    <van-cell title="Push Notifications" center>
      <template #right-icon>
        <van-switch v-model="pushEnabled" />
      </template>
    </van-cell>
    <van-cell title="Email Notifications" center>
      <template #right-icon>
        <van-switch v-model="emailEnabled" />
      </template>
    </van-cell>
  </van-cell-group>
</template>

<script setup>
import { ref } from 'vue'

const pushEnabled = ref(true)
const emailEnabled = ref(false)
</script>
```

### With Checkbox

```vue
<template>
  <van-cell-group title="Select Items">
    <van-cell
      v-for="item in items"
      :key="item.id"
      :title="item.title"
      clickable
      @click="toggleItem(item.id)"
    >
      <template #right-icon>
        <van-checkbox :ref="el => checkboxRefs[item.id] = el" />
      </template>
    </van-cell>
  </van-cell-group>
</template>

<script setup>
import { ref } from 'vue'

const items = ref([
  { id: 1, title: 'Item 1' },
  { id: 2, title: 'Item 2' },
  { id: 3, title: 'Item 3' },
])

const checkboxRefs = ref({})

const toggleItem = (id) => {
  checkboxRefs.value[id]?.toggle()
}
</script>
```

### With Badge

```vue
<template>
  <van-cell-group>
    <van-cell title="Messages" is-link>
      <template #value>
        <van-badge :content="5" />
      </template>
    </van-cell>
    <van-cell title="Notifications" is-link>
      <template #value>
        <van-badge dot />
      </template>
    </van-cell>
  </van-cell-group>
</template>
```

## Common Issues

### 1. Click Feedback Not Showing

Set `clickable` prop to enable click feedback:

```vue
<van-cell title="Clickable" clickable @click="handleClick" />
```

### 2. Custom Right Icon Not Aligned

Use the `right-icon` slot for custom icons:

```vue
<van-cell title="Title">
  <template #right-icon>
    <van-icon name="search" />
  </template>
</van-cell>
```

### 3. Cell Group Border Not Showing

Make sure `border` prop is not set to `false`:

```vue
<van-cell-group border>
  <van-cell title="Cell" />
</van-cell-group>
```

## Component Interactions

### With Form

```vue
<template>
  <van-cell-group title="User Info">
    <van-field v-model="username" label="Username" placeholder="Enter username" />
    <van-field v-model="email" label="Email" placeholder="Enter email" />
  </van-cell-group>
</template>

<script setup>
import { ref } from 'vue'

const username = ref('')
const email = ref('')
</script>
```

### With Popup

```vue
<template>
  <van-cell title="Select City" is-link @click="showPicker = true" />
  
  <van-popup v-model:show="showPicker" position="bottom">
    <van-picker :columns="cities" @confirm="onConfirm" />
  </van-popup>
</template>

<script setup>
import { ref } from 'vue'

const showPicker = ref(false)
const cities = ['Beijing', 'Shanghai', 'Guangzhou', 'Shenzhen']

const onConfirm = (value) => {
  showPicker.value = false
}
</script>
```

### With Swipe Cell

```vue
<template>
  <van-swipe-cell>
    <van-cell title="Cell" value="Content" />
    <template #right>
      <van-button square type="danger" text="Delete" />
    </template>
  </van-swipe-cell>
</template>
```

## Best Practices

1. **Group related cells**: Use CellGroup to organize related cells
2. **Use inset style**: Use inset style for better visual separation in mobile layouts
3. **Provide feedback**: Use clickable or is-link for interactive cells
4. **Consistent layout**: Use consistent size and layout across similar cells
5. **Accessibility**: Add meaningful titles and labels
6. **Icon usage**: Use icons to improve visual recognition
7. **Custom content**: Use slots for complex content layout
8. **Required fields**: Show required mark for mandatory fields in forms
