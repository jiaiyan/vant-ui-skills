---
name: "van-checkbox"
description: "Checkbox component for multiple selections. Invoke when user needs to implement checkboxes, checkbox groups, or custom checkbox styles."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Checkbox Component

A group of options for multiple choices with support for groups and custom styling.

## When to Invoke

Invoke this skill when:
- User needs to implement single or multiple checkboxes
- User wants to create checkbox groups
- User needs to limit the number of selections
- User wants to customize checkbox appearance
- User asks about toggle all functionality
- User needs indeterminate state

## Features

- **Checkbox Groups**: Group multiple checkboxes together
- **Custom Shape**: Round or square shapes
- **Custom Styling**: Color and size customization
- **Custom Icons**: Custom icon slots
- **Toggle All**: Select/deselect all in groups
- **Maximum Limit**: Limit the number of selections
- **Indeterminate State**: Partial selection state
- **Horizontal Layout**: Support for horizontal arrangement

## API Reference

### Checkbox Props

| Attribute | Description | Type | Default |
|-----------|-------------|------|---------|
| v-model | Check status | `boolean` | `false` |
| name | Checkbox name, usually a unique string or number | `any` | - |
| shape | Can be set to `square` | `string` | `round` |
| disabled | Disable checkbox | `boolean` | `false` |
| label-disabled | Whether to disable label click | `boolean` | `false` |
| label-position | Can be set to `left` | `string` | `right` |
| icon-size | Icon size | `number \| string` | `20px` |
| checked-color | Checked color | `string` | `#1989fa` |
| bind-group | Whether to bind with CheckboxGroup | `boolean` | `true` |
| indeterminate | Whether indeterminate status | `boolean` | `false` |

### CheckboxGroup Props

| Attribute | Description | Type | Default |
|-----------|-------------|------|---------|
| v-model | Names of all checked checkboxes | `any[]` | - |
| disabled | Whether to disable all checkboxes | `boolean` | `false` |
| max | Maximum amount of checked options | `number \| string` | `0`(Unlimited) |
| direction | Direction, can be set to `horizontal` | `string` | `vertical` |
| icon-size | Icon size of all checkboxes | `number \| string` | `20px` |
| checked-color | Checked color of all checkboxes | `string` | `#1989fa` |
| shape | Can be set to `square` | `string` | `round` |

### Checkbox Events

| Event | Description | Parameters |
|-------|-------------|------------|
| change | Emitted when value changed | `checked: boolean` |
| click | Emitted when the checkbox is clicked | `event: MouseEvent` |

### CheckboxGroup Events

| Event | Description | Parameters |
|-------|-------------|------------|
| change | Emitted when value changed | `names: any[]` |

### Checkbox Slots

| Name | Description | SlotProps |
|------|-------------|-----------|
| default | Custom label | `{ checked: boolean, disabled: boolean }` |
| icon | Custom icon | `{ checked: boolean, disabled: boolean }` |

### CheckboxGroup Methods

Use ref to get CheckboxGroup instance and call instance methods.

| Name | Description | Attribute | Return value |
|------|-------------|-----------|--------------|
| toggleAll | Toggle check status of all checkboxes | `options?: boolean \| object` | - |

### Checkbox Methods

Use ref to get Checkbox instance and call instance methods.

| Name | Description | Attribute | Return value |
|------|-------------|-----------|--------------|
| toggle | Toggle check status | `checked?: boolean` | - |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-checkbox v-model="checked">Checkbox</van-checkbox>
</template>

<script setup>
import { ref } from 'vue'

const checked = ref(true)
</script>
```

### Disabled

```vue
<template>
  <van-checkbox v-model="checked" disabled>Checkbox</van-checkbox>
</template>
```

### Custom Shape

```vue
<template>
  <van-checkbox-group v-model="checked" shape="square">
    <van-checkbox name="a">Checkbox a</van-checkbox>
    <van-checkbox name="b">Checkbox b</van-checkbox>
  </van-checkbox-group>
</template>

<script setup>
import { ref } from 'vue'

const checked = ref(['a', 'b'])
</script>
```

### Custom Color

```vue
<template>
  <van-checkbox v-model="checked" checked-color="#ee0a24">Checkbox</van-checkbox>
</template>
```

### Custom Icon Size

```vue
<template>
  <van-checkbox v-model="checked" icon-size="24px">Checkbox</van-checkbox>
</template>
```

### Custom Icon

```vue
<template>
  <van-checkbox v-model="checked">
    customize icon
    <template #icon="props">
      <img class="img-icon" :src="props.checked ? activeIcon : inactiveIcon" />
    </template>
  </van-checkbox>
</template>

<style>
.img-icon {
  height: 20px;
}
</style>

<script setup>
import { ref } from 'vue'

const checked = ref(true)
const activeIcon = 'https://fastly.jsdelivr.net/npm/@vant/assets/user-active.png'
const inactiveIcon = 'https://fastly.jsdelivr.net/npm/@vant/assets/user-inactive.png'
</script>
```

### Left Label

```vue
<template>
  <van-checkbox v-model="checked" label-position="left">Checkbox</van-checkbox>
</template>
```

### Checkbox Group

```vue
<template>
  <van-checkbox-group v-model="checked">
    <van-checkbox name="a">Checkbox a</van-checkbox>
    <van-checkbox name="b">Checkbox b</van-checkbox>
  </van-checkbox-group>
</template>

<script setup>
import { ref } from 'vue'

const checked = ref(['a', 'b'])
</script>
```

### Horizontal

```vue
<template>
  <van-checkbox-group v-model="checked" direction="horizontal">
    <van-checkbox name="a">Checkbox a</van-checkbox>
    <van-checkbox name="b">Checkbox b</van-checkbox>
  </van-checkbox-group>
</template>

<script setup>
import { ref } from 'vue'

const checked = ref([])
</script>
```

### Maximum Amount of Checked Options

```vue
<template>
  <van-checkbox-group v-model="checked" :max="2">
    <van-checkbox name="a">Checkbox a</van-checkbox>
    <van-checkbox name="b">Checkbox b</van-checkbox>
    <van-checkbox name="c">Checkbox c</van-checkbox>
  </van-checkbox-group>
</template>

<script setup>
import { ref } from 'vue'

const checked = ref([])
</script>
```

### Toggle All

```vue
<template>
  <van-checkbox-group v-model="checked" ref="checkboxGroup">
    <van-checkbox name="a">Checkbox a</van-checkbox>
    <van-checkbox name="b">Checkbox b</van-checkbox>
    <van-checkbox name="c">Checkbox c</van-checkbox>
  </van-checkbox-group>

  <van-button type="primary" @click="checkAll">Check All</van-button>
  <van-button type="primary" @click="toggleAll">Toggle All</van-button>
</template>

<script setup>
import { ref } from 'vue'

const checked = ref([])
const checkboxGroup = ref(null)

const checkAll = () => {
  checkboxGroup.value.toggleAll(true)
}

const toggleAll = () => {
  checkboxGroup.value.toggleAll()
}
</script>
```

### Inside a Cell

```vue
<template>
  <van-checkbox-group v-model="checked">
    <van-cell-group inset>
      <van-cell
        v-for="(item, index) in list"
        clickable
        :key="item"
        :title="`Checkbox ${item}`"
        @click="toggle(index)"
      >
        <template #right-icon>
          <van-checkbox
            :name="item"
            :ref="el => checkboxRefs[index] = el"
            @click.stop
          />
        </template>
      </van-cell>
    </van-cell-group>
  </van-checkbox-group>
</template>

<script setup>
import { ref, onBeforeUpdate } from 'vue'

const checked = ref([])
const checkboxRefs = ref([])
const list = ['a', 'b']

const toggle = (index) => {
  checkboxRefs.value[index].toggle()
}

onBeforeUpdate(() => {
  checkboxRefs.value = []
})
</script>
```

### Indeterminate

```vue
<template>
  <van-checkbox
    v-model="isCheckAll"
    :indeterminate="isIndeterminate"
    @change="checkAllChange"
  >
    Check All
  </van-checkbox>

  <van-checkbox-group v-model="checkedResult" @change="checkedResultChange">
    <van-checkbox v-for="item in list" :key="item" :name="item">
      Checkbox {{ item }}
    </van-checkbox>
  </van-checkbox-group>
</template>

<script setup>
import { ref } from 'vue'

const list = ['a', 'b', 'c', 'd']

const isCheckAll = ref(false)
const checkedResult = ref(['a', 'b', 'd'])
const isIndeterminate = ref(true)

const checkAllChange = (val) => {
  checkedResult.value = val ? list : []
  isIndeterminate.value = false
}

const checkedResultChange = (value) => {
  const checkedCount = value.length
  isCheckAll.value = checkedCount === list.length
  isIndeterminate.value = checkedCount > 0 && checkedCount < list.length
}
</script>
```

## Best Practices

1. **Use CheckboxGroup**: When multiple checkboxes need to be managed together, use CheckboxGroup for better state management.

2. **Unique Names**: Ensure each checkbox has a unique `name` when used in a group.

3. **Accessibility**: Provide clear labels for better accessibility.

4. **Toggle All**: Use `toggleAll` method for bulk operations, consider using `skipDisabled` option.

5. **Indeterminate State**: Use indeterminate state to indicate partial selection in hierarchical data.

6. **Mobile Optimization**: Consider using cells for better mobile touch experience.
