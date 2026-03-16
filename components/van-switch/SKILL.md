---
name: "van-switch"
description: "Switch component for toggling between on/off states. Invoke when user needs to implement toggle switches, settings controls, or boolean state toggles."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Switch Component

Switch component for toggling between on/off states with customizable appearance.

## When to Invoke

Invoke this skill when:
- User needs to implement a toggle switch
- User wants to create settings controls
- User needs async control for switch state
- User wants to customize switch appearance
- User asks about switch in cells or forms

## Features

- **Custom Colors**: Configurable active and inactive colors
- **Custom Size**: Adjustable switch size
- **Loading State**: Built-in loading indicator
- **Custom Values**: Custom active and inactive values
- **Custom Node**: Slot for custom node content
- **Custom Background**: Slot for custom background
- **Async Control**: Support for async state changes
- **Cell Integration**: Works seamlessly with Cell component

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model | Check status of Switch | `ActiveValue \| InactiveValue` | `false` |
| loading | Whether to show loading icon | `boolean` | `false` |
| disabled | Whether to disable switch | `boolean` | `false` |
| size | Size of switch button | `number \| string` | `26px` |
| active-color | Background color when active | `string` | `#1989fa` |
| inactive-color | Background color when inactive | `string` | `rgba(120, 120, 128, 0.16)` |
| active-value | Value when active | `any` | `true` |
| inactive-value | Value when inactive | `any` | `false` |

### Events

| Event | Description | Parameters |
|-------|-------------|------------|
| change | Emitted when check status changed | `value: any` |
| click | Emitted when component is clicked | `event: MouseEvent` |

### Slots

| Name | Description | SlotProps |
|------|-------------|-----------|
| node | Custom the content of node | - |
| background | Custom the background of switch | - |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-switch v-model="checked" />
</template>

<script setup>
import { ref } from 'vue'

const checked = ref(true)
</script>
```

### Disabled State

```vue
<template>
  <van-switch v-model="checked" disabled />
</template>

<script setup>
import { ref } from 'vue'

const checked = ref(true)
</script>
```

### Loading State

```vue
<template>
  <van-switch v-model="checked" loading />
</template>

<script setup>
import { ref } from 'vue'

const checked = ref(true)
</script>
```

### Custom Size

```vue
<template>
  <van-switch v-model="checked" size="22px" />
</template>

<script setup>
import { ref } from 'vue'

const checked = ref(true)
</script>
```

### Custom Color

```vue
<template>
  <van-switch 
    v-model="checked" 
    active-color="#ee0a24" 
    inactive-color="#dcdee0" 
  />
</template>

<script setup>
import { ref } from 'vue'

const checked = ref(true)
</script>
```

### Custom Node

```vue
<template>
  <van-switch v-model="checked">
    <template #node>
      <div class="icon-wrapper">
        <van-icon :name="checked ? 'success' : 'cross'" />
      </div>
    </template>
  </van-switch>
</template>

<script setup>
import { ref } from 'vue'

const checked = ref(true)
</script>

<style scoped>
.icon-wrapper {
  display: flex;
  width: 100%;
  justify-content: center;
  font-size: 18px;
}

.icon-wrapper .van-icon-success {
  line-height: 32px;
  color: var(--van-blue);
}

.icon-wrapper .van-icon-cross {
  line-height: 32px;
  color: var(--van-gray-5);
}
</style>
```

### Async Control

```vue
<template>
  <van-switch 
    :model-value="checked" 
    @update:model-value="onUpdateValue" 
  />
</template>

<script setup>
import { ref } from 'vue'
import { showConfirmDialog } from 'vant'

const checked = ref(true)

const onUpdateValue = (newValue) => {
  showConfirmDialog({
    title: 'Confirm',
    message: 'Are you sure to toggle switch?',
  }).then(() => {
    checked.value = newValue
  })
}
</script>
```

### Inside a Cell

```vue
<template>
  <van-cell center title="Title">
    <template #right-icon>
      <van-switch v-model="checked" />
    </template>
  </van-cell>
</template>

<script setup>
import { ref } from 'vue'

const checked = ref(true)
</script>
```

### Settings Page

```vue
<template>
  <div class="settings-page">
    <van-cell-group inset>
      <van-cell center title="Notifications">
        <template #right-icon>
          <van-switch v-model="settings.notifications" />
        </template>
      </van-cell>
      <van-cell center title="Dark Mode">
        <template #right-icon>
          <van-switch v-model="settings.darkMode" />
        </template>
      </van-cell>
      <van-cell center title="Auto Update">
        <template #right-icon>
          <van-switch v-model="settings.autoUpdate" />
        </template>
      </van-cell>
      <van-cell center title="Location Services">
        <template #right-icon>
          <van-switch 
            v-model="settings.location" 
            :loading="locationLoading"
            @change="onLocationChange"
          />
        </template>
      </van-cell>
    </van-cell-group>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const settings = ref({
  notifications: true,
  darkMode: false,
  autoUpdate: true,
  location: false
})

const locationLoading = ref(false)

const onLocationChange = async (value) => {
  locationLoading.value = true
  setTimeout(() => {
    locationLoading.value = false
    showToast(value ? 'Location enabled' : 'Location disabled')
  }, 1000)
}
</script>

<style scoped>
.settings-page {
  padding: 16px;
  background: #f7f8fa;
  min-height: 100vh;
}
</style>
```

### With Form

```vue
<template>
  <van-form @submit="onSubmit">
    <van-field name="switch" label="Switch">
      <template #input>
        <van-switch v-model="checked" />
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

const checked = ref(false)

const onSubmit = () => {
  showToast('Switch: ' + checked.value)
}
</script>
```

### Custom Values

```vue
<template>
  <van-switch 
    v-model="status" 
    active-value="on" 
    inactive-value="off"
    @change="onStatusChange"
  />
  <p>Status: {{ status }}</p>
</template>

<script setup>
import { ref } from 'vue'

const status = ref('on')

const onStatusChange = (value) => {
  console.log('Status changed to:', value)
}
</script>
```

### Async Toggle with Confirmation

```vue
<template>
  <van-cell center title="Enable Feature">
    <template #right-icon>
      <van-switch 
        :model-value="enabled" 
        :loading="loading"
        @update:model-value="toggleFeature"
      />
    </template>
  </van-cell>
</template>

<script setup>
import { ref } from 'vue'
import { showConfirmDialog, showToast } from 'vant'

const enabled = ref(false)
const loading = ref(false)

const toggleFeature = async (newValue) => {
  try {
    await showConfirmDialog({
      title: 'Confirm',
      message: `Are you sure you want to ${newValue ? 'enable' : 'disable'} this feature?`,
    })
    
    loading.value = true
    
    await new Promise(resolve => setTimeout(resolve, 1000))
    
    enabled.value = newValue
    showToast(newValue ? 'Feature enabled' : 'Feature disabled')
  } catch {
    // User cancelled
  } finally {
    loading.value = false
  }
}
</script>
```

## Best Practices

1. **Clear Labels**: Provide clear labels for switch purpose
2. **Loading State**: Show loading during async operations
3. **Confirmation**: Use confirmation dialogs for important toggles
4. **Custom Values**: Use custom values for non-boolean states
5. **Cell Integration**: Use with Cell for better mobile UX
6. **Accessibility**: Ensure switches are properly labeled
7. **Visual Feedback**: Use appropriate colors for active/inactive states
8. **Error Handling**: Handle errors in async toggle operations
