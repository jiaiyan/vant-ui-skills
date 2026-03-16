---
name: "van-tab"
description: "Tab component for switching between different content areas. Invoke when user needs to implement tabbed interfaces with multiple panels."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Tab Component

Tab component used to switch between different content areas, supporting various styles and interactions.

## When to Invoke

Invoke this skill when:
- User needs to implement a tabbed interface
- User wants to switch between different content panels
- User needs sticky tabs or swipeable content
- User wants to implement card-style tabs
- User asks about lazy rendering or scrollspy mode

## Features

- **Multiple Styles**: Line style and card style
- **Sticky Mode**: Tabs stick to top when scrolling
- **Swipeable**: Swipe to switch tabs
- **Animated**: Smooth transition animations
- **Lazy Rendering**: Render content on demand
- **Scrollspy**: Scroll to activate tabs
- **Badge Support**: Show badges on tab titles
- **Custom Content**: Full customization via slots

## API Reference

### Tabs Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model:active | Index of active tab | `number \| string` | `0` |
| type | Style type: `line` or `card` | `string` | `line` |
| color | Tab color | `string` | `#1989fa` |
| background | Background color | `string` | `white` |
| duration | Animation duration | `number \| string` | `0.3` |
| line-width | Width of tab line | `number \| string` | `40px` |
| line-height | Height of tab line | `number \| string` | `3px` |
| animated | Whether to animate tab changes | `boolean` | `false` |
| border | Whether to show border (line type) | `boolean` | `false` |
| ellipsis | Whether to ellipsis long titles | `boolean` | `true` |
| sticky | Whether to use sticky mode | `boolean` | `false` |
| shrink | Whether to shrink tabs left | `boolean` | `false` |
| swipeable | Whether to enable swipe gesture | `boolean` | `false` |
| lazy-render | Whether to enable lazy render | `boolean` | `true` |
| scrollspy | Whether to use scrollspy mode | `boolean` | `false` |
| show-header | Whether to show title bar | `boolean` | `true` |
| offset-top | Sticky offset top | `number \| string` | `0` |
| swipe-threshold | Swipe tabs threshold | `number \| string` | `5` |
| title-active-color | Active title color | `string` | - |
| title-inactive-color | Inactive title color | `string` | - |
| before-change | Callback before changing tabs | `(name) => boolean \| Promise<boolean>` | - |

### Tab Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| title | Tab title | `string` | - |
| disabled | Whether to disable tab | `boolean` | `false` |
| dot | Whether to show red dot | `boolean` | `false` |
| badge | Badge content | `number \| string` | - |
| name | Tab identifier | `number \| string` | Tab index |
| url | Link URL | `string` | - |
| to | Target route object | `string \| object` | - |
| replace | Whether to replace history | `boolean` | `false` |
| title-style | Custom title style | `string \| Array \| object` | - |
| title-class | Custom title class | `string \| Array \| object` | - |
| show-zero-badge | Show badge when value is zero | `boolean` | `true` |

### Tabs Events

| Name | Description | Arguments |
|------|-------------|-----------|
| click-tab | Emitted when tab is clicked | `{ name, title, event, disabled }` |
| change | Emitted when active tab changes | `name, title` |
| rendered | Emitted when content renders (lazy mode) | `name, title` |
| scroll | Emitted when tab scrolls (sticky mode) | `{ scrollTop, isFixed }` |

### Tabs Methods

| Name | Description | Arguments | Return Value |
|------|-------------|-----------|--------------|
| resize | Resize tabs | - | - |
| scrollTo | Scroll to specified tab (scrollspy) | `name: string \| number` | - |

### Tabs Slots

| Name | Description |
|------|-------------|
| nav-left | Custom nav left content |
| nav-right | Custom nav right content |
| nav-bottom | Custom nav bottom content |

### Tab Slots

| Name | Description |
|------|-------------|
| default | Tab content |
| title | Custom tab title |

### Types

```ts
import type { TabProps, TabsType, TabsProps, TabsInstance } from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-tabs v-model:active="active">
    <van-tab v-for="index in 4" :key="index" :title="`Tab ${index}`">
      Content of tab {{ index }}
    </van-tab>
  </van-tabs>
</template>

<script setup>
import { ref } from 'vue';

const active = ref(0);
</script>
```

### Match By Name

```vue
<template>
  <van-tabs v-model:active="activeName">
    <van-tab title="Tab 1" name="a">Content of tab 1</van-tab>
    <van-tab title="Tab 2" name="b">Content of tab 2</van-tab>
    <van-tab title="Tab 3" name="c">Content of tab 3</van-tab>
  </van-tabs>
</template>

<script setup>
import { ref } from 'vue';

const activeName = ref('b');
</script>
```

### Card Style

```vue
<template>
  <van-tabs v-model:active="active" type="card">
    <van-tab v-for="index in 3" :key="index" :title="`Tab ${index}`">
      Content of tab {{ index }}
    </van-tab>
  </van-tabs>
</template>

<script setup>
import { ref } from 'vue';

const active = ref(0);
</script>
```

### Sticky Tabs

```vue
<template>
  <van-tabs v-model:active="active" sticky>
    <van-tab v-for="index in 4" :key="index" :title="`Tab ${index}`">
      Content of tab {{ index }}
    </van-tab>
  </van-tabs>
</template>

<script setup>
import { ref } from 'vue';

const active = ref(0);
</script>
```

### Swipeable

```vue
<template>
  <van-tabs v-model:active="active" swipeable>
    <van-tab v-for="index in 4" :key="index" :title="`Tab ${index}`">
      Content of tab {{ index }}
    </van-tab>
  </van-tabs>
</template>

<script setup>
import { ref } from 'vue';

const active = ref(0);
</script>
```

### Animated

```vue
<template>
  <van-tabs v-model:active="active" animated>
    <van-tab v-for="index in 4" :key="index" :title="`Tab ${index}`">
      Content of tab {{ index }}
    </van-tab>
  </van-tabs>
</template>

<script setup>
import { ref } from 'vue';

const active = ref(0);
</script>
```

### Disabled Tab

```vue
<template>
  <van-tabs v-model:active="active">
    <van-tab v-for="index in 3" :key="index" :title="`Tab ${index}`" :disabled="index === 2">
      Content of tab {{ index }}
    </van-tab>
  </van-tabs>
</template>

<script setup>
import { ref } from 'vue';

const active = ref(0);
</script>
```

### Custom Tab Title

```vue
<template>
  <van-tabs v-model:active="active">
    <van-tab v-for="index in 2" :key="index">
      <template #title>
        <van-icon name="more-o" />
        Tab {{ index }}
      </template>
      Content of tab {{ index }}
    </van-tab>
  </van-tabs>
</template>

<script setup>
import { ref } from 'vue';

const active = ref(0);
</script>
```

### Before Change

```vue
<template>
  <van-tabs v-model:active="active" :before-change="beforeChange">
    <van-tab v-for="index in 4" :key="index" :title="`Tab ${index}`">
      Content of tab {{ index }}
    </van-tab>
  </van-tabs>
</template>

<script setup>
import { ref } from 'vue';

const active = ref(0);

const beforeChange = (index) => {
  if (index === 1) {
    return false;
  }
  return new Promise((resolve) => {
    setTimeout(() => resolve(index !== 3), 1000);
  });
};
</script>
```

### Scrollspy Mode

```vue
<template>
  <van-tabs v-model:active="active" scrollspy sticky>
    <van-tab v-for="index in 8" :key="index" :title="`Tab ${index}`">
      <div style="height: 200px">Content of tab {{ index }}</div>
    </van-tab>
  </van-tabs>
</template>

<script setup>
import { ref } from 'vue';

const active = ref(0);
</script>
```

## Best Practices

1. **Use lazy-render**: Enable `lazy-render` for better performance with many tabs
2. **Sticky with offset**: Set `offset-top` when using sticky with fixed headers
3. **Swipeable for mobile**: Enable `swipeable` for better mobile experience
4. **Limit tab count**: Keep tabs under 5-7 for better usability
5. **Use before-change**: Validate before switching tabs
6. **Avoid sticky in animated**: Sticky elements inside animated tabs may have issues
