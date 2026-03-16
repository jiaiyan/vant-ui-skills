---
name: "van-sidebar"
description: "Sidebar navigation component for switching between content areas. Invoke when user needs to implement vertical navigation sidebar."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Sidebar Component

A vertically displayed navigation bar used to switch between different content areas.

## When to Invoke

Invoke this skill when:
- User needs to implement a vertical navigation sidebar
- User wants to switch between different content sections
- User needs to show badges on navigation items
- User wants to create a category navigation
- User asks about sidebar with disabled items

## Features

- **Vertical Navigation**: Display navigation items vertically
- **Active State**: Highlight the active navigation item
- **Badge Support**: Show dot or number badges on items
- **Disabled Items**: Disable specific navigation items
- **Router Navigation**: Navigate to routes or URLs
- **Custom Content**: Customize item content via slots

## API Reference

### Sidebar Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model | Index of chosen item | `number \| string` | `0` |

### Sidebar Events

| Name | Description | Arguments |
|------|-------------|-----------|
| change | Emitted when chosen item changes | `index: number` |

### SidebarItem Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| title | Item content text | `string` | `''` |
| dot | Whether to show red dot | `boolean` | `false` |
| badge | Content of the badge | `number \| string` | `''` |
| badge-props | Props of Badge component | `BadgeProps` | - |
| disabled | Whether to disable item | `boolean` | `false` |
| url | Link URL | `string` | - |
| to | Target route object | `string \| object` | - |
| replace | Whether to replace history | `boolean` | `false` |

### SidebarItem Events

| Name | Description | Arguments |
|------|-------------|-----------|
| click | Emitted when item is clicked | `index: number` |

### SidebarItem Slots

| Name | Description |
|------|-------------|
| title | Custom item title |

### Types

```ts
import type { SidebarProps, SidebarItemProps } from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-sidebar v-model="active">
    <van-sidebar-item title="Category 1" />
    <van-sidebar-item title="Category 2" />
    <van-sidebar-item title="Category 3" />
  </van-sidebar>
</template>

<script setup>
import { ref } from 'vue';

const active = ref(0);
</script>
```

### Show Badge

```vue
<template>
  <van-sidebar v-model="active">
    <van-sidebar-item title="Category 1" dot />
    <van-sidebar-item title="Category 2" badge="5" />
    <van-sidebar-item title="Category 3" />
  </van-sidebar>
</template>

<script setup>
import { ref } from 'vue';

const active = ref(0);
</script>
```

### Disabled Items

```vue
<template>
  <van-sidebar v-model="active">
    <van-sidebar-item title="Category 1" />
    <van-sidebar-item title="Category 2" disabled />
    <van-sidebar-item title="Category 3" />
  </van-sidebar>
</template>

<script setup>
import { ref } from 'vue';

const active = ref(0);
</script>
```

### With Change Event

```vue
<template>
  <van-sidebar v-model="active" @change="onChange">
    <van-sidebar-item title="Category 1" />
    <van-sidebar-item title="Category 2" />
    <van-sidebar-item title="Category 3" />
  </van-sidebar>
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const active = ref(0);

const onChange = (index) => {
  showToast(`Selected Category ${index + 1}`);
};
</script>
```

### With Content Area

```vue
<template>
  <div class="sidebar-demo">
    <van-sidebar v-model="active" class="sidebar">
      <van-sidebar-item title="Category 1" />
      <van-sidebar-item title="Category 2" />
      <van-sidebar-item title="Category 3" />
    </van-sidebar>
    <div class="content">
      <div v-if="active === 0">Content for Category 1</div>
      <div v-if="active === 1">Content for Category 2</div>
      <div v-if="active === 2">Content for Category 3</div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const active = ref(0);
</script>

<style>
.sidebar-demo {
  display: flex;
}
.sidebar {
  width: 85px;
}
.content {
  flex: 1;
  padding: 20px;
}
</style>
```

### Router Navigation

```vue
<template>
  <van-sidebar v-model="active">
    <van-sidebar-item title="Home" to="/" />
    <van-sidebar-item title="Products" to="/products" />
    <van-sidebar-item title="About" to="/about" />
  </van-sidebar>
</template>

<script setup>
import { ref } from 'vue';

const active = ref(0);
</script>
```

### Custom Title

```vue
<template>
  <van-sidebar v-model="active">
    <van-sidebar-item>
      <template #title>
        <van-icon name="home-o" />
        <span>Home</span>
      </template>
    </van-sidebar-item>
    <van-sidebar-item>
      <template #title>
        <van-icon name="search" />
        <span>Search</span>
      </template>
    </van-sidebar-item>
  </van-sidebar>
</template>

<script setup>
import { ref } from 'vue';

const active = ref(0);
</script>
```

## Best Practices

1. **Combine with content**: Use sidebar with a content area for category navigation
2. **Show badges**: Display badges for items with notifications
3. **Limit items**: Keep sidebar items under 10 for better UX
4. **Disabled state**: Use disabled for unavailable categories
5. **Consistent styling**: Match sidebar width with your layout
6. **Active indication**: Ensure active state is clearly visible
