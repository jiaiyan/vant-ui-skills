---
name: "van-pagination"
description: "Pagination component for separating large datasets into pages. Invoke when user needs to implement page navigation for data lists."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Pagination Component

Pagination component used when the amount of data is too much, separating the data and loading only one page at a time.

## When to Invoke

Invoke this skill when:
- User needs to implement pagination for data lists
- User wants to navigate between pages of content
- User needs to customize pagination appearance
- User wants to show ellipses for large page counts
- User asks about page change events or custom buttons

## Features

- **Multiple Modes**: Multi-page mode and simple mode
- **Ellipsis Support**: Show ellipses for large page counts
- **Custom Buttons**: Customize prev/next button content
- **Page Slots**: Custom page item rendering
- **Total Items**: Calculate pages from total items and items per page
- **Force Ellipses**: Always show ellipses for better UX

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model | Current page number | `number` | - |
| mode | Mode: `simple` or `multi` | `string` | `multi` |
| prev-text | Previous button text | `string` | `Previous` |
| next-text | Next button text | `string` | `Next` |
| total-items | Total number of items | `number \| string` | `0` |
| items-per-page | Items per page | `number \| string` | `10` |
| page-count | Total page count (overrides calculation) | `number \| string` | - |
| show-page-size | Count of page buttons to show | `number \| string` | `5` |
| force-ellipses | Whether to show ellipses | `boolean` | `false` |
| show-prev-button | Whether to show prev button | `boolean` | `true` |
| show-next-button | Whether to show next button | `boolean` | `true` |

### Events

| Name | Description | Arguments |
|------|-------------|-----------|
| change | Emitted when current page changes | - |

### Slots

| Name | Description | SlotProps |
|------|-------------|-----------|
| page | Custom pagination item | `{ number: number, text: string, active: boolean }` |
| prev-text | Custom prev text | - |
| next-text | Custom next text | - |

### Types

```ts
import type { PaginationMode, PaginationProps } from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-pagination 
    v-model="currentPage" 
    :total-items="24" 
    :items-per-page="5" 
  />
</template>

<script setup>
import { ref } from 'vue';

const currentPage = ref(1);
</script>
```

### Simple Mode

```vue
<template>
  <van-pagination 
    v-model="currentPage" 
    :page-count="12" 
    mode="simple" 
  />
</template>

<script setup>
import { ref } from 'vue';

const currentPage = ref(1);
</script>
```

### Show Ellipses

```vue
<template>
  <van-pagination
    v-model="currentPage"
    :total-items="125"
    :show-page-size="3"
    force-ellipses
  />
</template>

<script setup>
import { ref } from 'vue';

const currentPage = ref(1);
</script>
```

### Custom Buttons

```vue
<template>
  <van-pagination 
    v-model="currentPage" 
    :total-items="50" 
    :show-page-size="5"
  >
    <template #prev-text>
      <van-icon name="arrow-left" />
    </template>
    <template #next-text>
      <van-icon name="arrow" />
    </template>
    <template #page="{ text }">{{ text }}</template>
  </van-pagination>
</template>

<script setup>
import { ref } from 'vue';

const currentPage = ref(1);
</script>
```

### With Change Event

```vue
<template>
  <van-pagination 
    v-model="currentPage" 
    :total-items="100" 
    :items-per-page="10"
    @change="onPageChange"
  />
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const currentPage = ref(1);

const onPageChange = () => {
  showToast(`Page changed to ${currentPage.value}`);
  // Fetch data for the new page
  fetchData(currentPage.value);
};

const fetchData = (page) => {
  console.log('Fetching data for page:', page);
};
</script>
```

### Hide Navigation Buttons

```vue
<template>
  <van-pagination 
    v-model="currentPage" 
    :total-items="50"
    :show-prev-button="false"
    :show-next-button="false"
  />
</template>

<script setup>
import { ref } from 'vue';

const currentPage = ref(1);
</script>
```

### Custom Page Count

```vue
<template>
  <van-pagination 
    v-model="currentPage" 
    :page-count="20"
  />
</template>

<script setup>
import { ref } from 'vue';

const currentPage = ref(1);
</script>
```

## Best Practices

1. **Use appropriate mode**: Use `simple` mode for mobile, `multi` for desktop
2. **Show ellipses**: Enable `force-ellipses` for better navigation with many pages
3. **Calculate pages**: Use `total-items` and `items-per-page` for dynamic data
4. **Custom buttons**: Use icons for prev/next buttons on mobile
5. **Page change handling**: Always handle the `change` event to fetch new data
6. **Limit show-page-size**: Keep `show-page-size` reasonable (3-7) for better UX
