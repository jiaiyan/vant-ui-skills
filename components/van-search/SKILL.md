---
name: "van-search"
description: "Search component for search scenarios with input and action buttons. Invoke when user needs to implement search functionality, search bars, or custom search inputs."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Search Component

Search component for search scenarios with customizable input and action buttons.

## When to Invoke

Invoke this skill when:
- User needs to implement a search bar
- User wants to create search functionality with filters
- User needs custom action buttons in search
- User wants to customize search input appearance
- User asks about search events and keyboard interactions

## Features

- **Flexible Shape**: Square or round search bar
- **Custom Background**: Configurable background color
- **Action Button**: Optional action button with customizable text
- **Input Alignment**: Left, center, or right text alignment
- **Clear Button**: Built-in clear functionality
- **Custom Icons**: Customizable left and right icons
- **Formatter**: Input value formatting support
- **Form Integration**: Works with HTML forms for iOS keyboard optimization

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model | Input value | `number \| string` | - |
| label | Left side label | `string` | - |
| name | As the identifier when submitting the form | `string` | - |
| shape | Shape of field, can be set to `round` | `string` | `square` |
| id | Input id | `string` | `van-search-n-input` |
| background | Background color of field | `string` | `#f2f2f2` |
| maxlength | Max length of value | `number \| string` | - |
| placeholder | Placeholder | `string` | - |
| clearable | Whether to be clearable | `boolean` | `true` |
| clear-icon | Clear icon name | `string` | `clear` |
| clear-trigger | When to display the clear icon | `string` | `focus` |
| autofocus | Whether to auto focus | `boolean` | `false` |
| show-action | Whether to show right action button | `boolean` | `false` |
| action-text | Text of action button | `string` | `Cancel` |
| disabled | Whether to disable field | `boolean` | `false` |
| readonly | Whether to be readonly | `boolean` | `false` |
| error | Whether to mark the input content in red | `boolean` | `false` |
| error-message | Error message | `string` | - |
| formatter | Input value formatter | `(val: string) => string` | - |
| format-trigger | When to format value | `string` | `onChange` |
| input-align | Text align of field | `string` | `left` |
| left-icon | Left icon name | `string` | `search` |
| right-icon | Right icon name | `string` | - |
| autocomplete | Autocomplete attribute of native input | `string` | - |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| search | Emitted when confirming search | `value: string` |
| update:model-value | Emitted when input value changed | `value: string` |
| focus | Emitted when input is focused | `event: Event` |
| blur | Emitted when input is blurred | `event: Event` |
| click-input | Emitted when the input is clicked | `event: MouseEvent` |
| click-left-icon | Emitted when the left icon is clicked | `event: MouseEvent` |
| click-right-icon | Emitted when the right icon is clicked | `event: MouseEvent` |
| clear | Emitted when the clear icon is clicked | `event: MouseEvent` |
| cancel | Emitted when the cancel button is clicked | - |

### Methods

| Name | Description | Attribute | Return value |
|------|-------------|-----------|--------------|
| focus | Trigger input focus | - | - |
| blur | Trigger input blur | - | - |

### Slots

| Name | Description |
|------|-------------|
| left | Custom left side content |
| action | Custom right button, displayed when `show-action` is `true` |
| label | Custom Search label |
| left-icon | Custom left icon |
| right-icon | Custom right icon |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-search v-model="value" placeholder="Placeholder" />
</template>

<script setup>
import { ref } from 'vue'

const value = ref('')
</script>
```

### Listen to Events

```vue
<template>
  <form action="/">
    <van-search
      v-model="value"
      show-action
      placeholder="Placeholder"
      @search="onSearch"
      @cancel="onCancel"
    />
  </form>
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const value = ref('')

const onSearch = (val) => {
  showToast(val)
}

const onCancel = () => {
  showToast('Cancel')
}
</script>
```

### Input Align

```vue
<template>
  <van-search v-model="value" input-align="center" placeholder="Placeholder" />
</template>

<script setup>
import { ref } from 'vue'

const value = ref('')
</script>
```

### Disabled State

```vue
<template>
  <van-search v-model="value" disabled placeholder="Placeholder" />
</template>

<script setup>
import { ref } from 'vue'

const value = ref('')
</script>
```

### Custom Background Color

```vue
<template>
  <van-search
    v-model="value"
    shape="round"
    background="#4fc08d"
    placeholder="Placeholder"
  />
</template>

<script setup>
import { ref } from 'vue'

const value = ref('')
</script>
```

### Custom Action Button

```vue
<template>
  <van-search
    v-model="value"
    show-action
    label="Address"
    placeholder="Placeholder"
    @search="onSearch"
  >
    <template #action>
      <div @click="onClickButton">Search</div>
    </template>
  </van-search>
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const value = ref('')

const onSearch = (val) => {
  showToast(val)
}

const onClickButton = () => {
  showToast(value.value)
}
</script>
```

### Search with History

```vue
<template>
  <div class="search-page">
    <van-search
      v-model="value"
      show-action
      placeholder="Search products"
      @search="onSearch"
      @cancel="onCancel"
    />
    
    <div v-if="!value && searchHistory.length" class="search-history">
      <div class="history-header">
        <span>Search History</span>
        <van-icon name="delete-o" @click="clearHistory" />
      </div>
      <van-tag 
        v-for="(item, index) in searchHistory" 
        :key="index"
        size="large"
        @click="searchFromHistory(item)"
      >
        {{ item }}
      </van-tag>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const value = ref('')
const searchHistory = ref(['Apple', 'Banana', 'Orange'])

const onSearch = (val) => {
  if (val && !searchHistory.value.includes(val)) {
    searchHistory.value.unshift(val)
  }
  showToast('Searching: ' + val)
}

const onCancel = () => {
  value.value = ''
}

const clearHistory = () => {
  searchHistory.value = []
  showToast('History cleared')
}

const searchFromHistory = (item) => {
  value.value = item
  onSearch(item)
}
</script>

<style scoped>
.search-page {
  background: #f7f8fa;
  min-height: 100vh;
}

.search-history {
  padding: 16px;
}

.history-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 12px;
  font-size: 14px;
  color: #323233;
}

.van-tag {
  margin-right: 8px;
  margin-bottom: 8px;
}
</style>
```

### Search with Results

```vue
<template>
  <div>
    <van-search
      v-model="value"
      show-action
      placeholder="Search"
      @search="onSearch"
      @cancel="onCancel"
    />
    
    <van-list v-if="showResults">
      <van-cell 
        v-for="item in results" 
        :key="item.id" 
        :title="item.title"
        @click="onSelect(item)"
      />
    </van-list>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const value = ref('')
const showResults = ref(false)
const results = ref([])

const onSearch = (val) => {
  results.value = [
    { id: 1, title: `Result 1 for "${val}"` },
    { id: 2, title: `Result 2 for "${val}"` },
    { id: 3, title: `Result 3 for "${val}"` },
  ]
  showResults.value = true
}

const onCancel = () => {
  value.value = ''
  showResults.value = false
  results.value = []
}

const onSelect = (item) => {
  console.log('Selected:', item)
}
</script>
```

### Using Methods

```vue
<template>
  <div>
    <van-search 
      ref="searchRef"
      v-model="value" 
      placeholder="Placeholder" 
    />
    <van-button @click="focusInput">Focus</van-button>
    <van-button @click="blurInput">Blur</van-button>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const value = ref('')
const searchRef = ref()

const focusInput = () => {
  searchRef.value?.focus()
}

const blurInput = () => {
  searchRef.value?.blur()
}
</script>
```

## Best Practices

1. **Form Wrapper**: Wrap in `<form>` for iOS keyboard search button
2. **Debounce**: Implement debouncing for search-as-you-type
3. **Clear History**: Provide option to clear search history
4. **Loading State**: Show loading indicator during search
5. **Empty State**: Handle empty search results gracefully
6. **Keyboard Type**: Use appropriate keyboard types for different contexts
7. **Autocomplete**: Enable autocomplete for better UX
8. **Accessibility**: Ensure proper labels and ARIA attributes
