---
name: "van-popover"
description: "Popover component for displaying floating content. Invoke when user needs to implement dropdown menus, tooltips, or floating action panels."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Popover Component

Used to display some content on top of another element.

## When to Invoke

Invoke this skill when:
- User needs to implement dropdown menus
- User wants to create floating action panels
- User needs to display tooltips or hints
- User wants to show contextual menus
- User asks about popover positioning and themes

## Features

- **Multiple Themes**: Light and dark themes
- **Flexible Placement**: 12 placement positions
- **Action List**: Built-in action list support
- **Horizontal/Vertical**: Action layout direction
- **Custom Content**: Full content customization via slots
- **Controlled/Uncontrolled**: Support both modes
- **Icon Support**: Icons for each action item

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model:show | Whether to show Popover | `boolean` | `false` |
| actions | Actions | `PopoverAction[]` | `[]` |
| actions-direction | Direction of actions | `PopoverActionsDirection` | `vertical` |
| placement | Placement | `PopoverPlacement` | `bottom` |
| theme | Theme, can be set to `dark` | `PopoverTheme` | `light` |
| trigger | Trigger mode, can be set to `manual` | `PopoverTrigger` | `click` |
| duration | Transition duration, unit second | `number \| string` | `0.3` |
| offset | Distance to reference | `[number, number]` | `[0, 8]` |
| overlay | Whether to show overlay | `boolean` | `false` |
| overlay-class | Custom overlay class | `string \| Array \| object` | - |
| overlay-style | Custom overlay style | `object` | - |
| show-arrow | Whether to show arrow | `boolean` | `true` |
| close-on-click-action | Whether to close when clicking action | `boolean` | `true` |
| close-on-click-outside | Whether to close when clicking outside | `boolean` | `true` |
| close-on-click-overlay | Whether to close when clicking overlay | `boolean` | `true` |
| teleport | Specifies a target element | `string \| Element` | `body` |
| icon-prefix | Icon className prefix | `string` | `van-icon` |

### PopoverAction Structure

| Key | Description | Type |
|-----|-------------|------|
| text | Action Text | `string` |
| icon | Icon | `string` |
| color | Action Color | `string` |
| disabled | Whether to be disabled | `boolean` |
| className | className of the option | `string \| Array \| object` |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| select | Emitted when an action is clicked | `action: PopoverAction, index: number` |
| open | Emitted when opening Popover | - |
| close | Emitted when closing Popover | - |
| opened | Emitted when Popover is opened | - |
| closed | Emitted when Popover is closed | - |
| click-overlay | Emitted when overlay is clicked | `event: MouseEvent` |

### Slots

| Name | Description | SlotProps |
|------|-------------|-----------|
| default | Custom content | - |
| reference | Reference Element | - |
| action | Custom the content of option | `{ action: PopoverAction, index: number }` |

### Types

```ts
import type {
  PopoverProps,
  PopoverTheme,
  PopoverAction,
  PopoverActionsDirection,
  PopoverTrigger,
  PopoverPlacement,
} from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-popover v-model:show="showPopover" :actions="actions" @select="onSelect">
    <template #reference>
      <van-button type="primary">Light Theme</van-button>
    </template>
  </van-popover>
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const showPopover = ref(false);
const actions = [
  { text: 'Option 1' },
  { text: 'Option 2' },
  { text: 'Option 3' },
];

const onSelect = (action) => showToast(action.text);
</script>
```

### Dark Theme

```vue
<template>
  <van-popover v-model:show="showPopover" theme="dark" :actions="actions">
    <template #reference>
      <van-button type="primary">Dark Theme</van-button>
    </template>
  </van-popover>
</template>

<script setup>
import { ref } from 'vue';

const showPopover = ref(false);
const actions = [
  { text: 'Option 1' },
  { text: 'Option 2' },
  { text: 'Option 3' },
];
</script>
```

### Horizontal Layout

```vue
<template>
  <van-popover
    v-model:show="showPopover"
    :actions="actions"
    actions-direction="horizontal"
  >
    <template #reference>
      <van-button type="primary">Horizontal</van-button>
    </template>
  </van-popover>
</template>
```

### Placement Options

```vue
<template>
  <van-popover placement="top" />
</template>
```

Available placements:
- `top`, `top-start`, `top-end`
- `left`, `left-start`, `left-end`
- `right`, `right-start`, `right-end`
- `bottom`, `bottom-start`, `bottom-end`

### With Icons

```vue
<template>
  <van-popover v-model:show="showPopover" :actions="actions">
    <template #reference>
      <van-button type="primary">Show Icon</van-button>
    </template>
  </van-popover>
</template>

<script setup>
import { ref } from 'vue';

const showPopover = ref(false);
const actions = [
  { text: 'Option 1', icon: 'add-o' },
  { text: 'Option 2', icon: 'music-o' },
  { text: 'Option 3', icon: 'more-o' },
];
</script>
```

### Disabled Action

```vue
<template>
  <van-popover v-model:show="showPopover" :actions="actions">
    <template #reference>
      <van-button type="primary">Disable Action</van-button>
    </template>
  </van-popover>
</template>

<script setup>
import { ref } from 'vue';

const showPopover = ref(false);
const actions = [
  { text: 'Option 1', disabled: true },
  { text: 'Option 2', disabled: true },
  { text: 'Option 3' },
];
</script>
```

### Custom Content

```vue
<template>
  <van-popover v-model:show="showPopover">
    <van-grid
      square
      clickable
      :border="false"
      column-num="3"
      style="width: 240px;"
    >
      <van-grid-item
        v-for="i in 6"
        :key="i"
        text="Option"
        icon="photo-o"
        @click="showPopover = false"
      />
    </van-grid>
    <template #reference>
      <van-button type="primary">Custom Content</van-button>
    </template>
  </van-popover>
</template>

<script setup>
import { ref } from 'vue';

const showPopover = ref(false);
</script>
```

### Uncontrolled Mode

```vue
<template>
  <van-popover :actions="actions" placement="top-start" @select="onSelect">
    <template #reference>
      <van-button type="primary">Uncontrolled</van-button>
    </template>
  </van-popover>
</template>

<script setup>
import { showToast } from 'vant';

const actions = [
  { text: 'Option 1' },
  { text: 'Option 2' },
  { text: 'Option 3' },
];

const onSelect = (action) => showToast(action.text);
</script>
```

## Common Issues

### 1. Popover Not Showing

Ensure `v-model:show` is properly bound:

```vue
<van-popover v-model:show="showPopover">
  <template #reference>
    <van-button @click="showPopover = true">Show</van-button>
  </template>
</van-popover>
```

### 2. Manual Trigger

Use `trigger="manual"` for programmatic control:

```vue
<van-popover v-model:show="show" trigger="manual">
  <template #reference>
    <van-button>Reference</van-button>
  </template>
</van-popover>
```

### 3. Preventing Close

Set `close-on-click-action` to false:

```vue
<van-popover
  v-model:show="show"
  :actions="actions"
  :close-on-click-action="false"
/>
```

## Component Interactions

### With Navigation Bar

```vue
<template>
  <van-nav-bar title="Title">
    <template #right>
      <van-popover :actions="actions" @select="onSelect">
        <template #reference>
          <van-icon name="ellipsis" size="20" />
        </template>
      </van-popover>
    </template>
  </van-nav-bar>
</template>
```

### With Context Menu

```vue
<template>
  <div @contextmenu.prevent="showMenu">
    Right click here
    <van-popover
      v-model:show="showPopover"
      :actions="actions"
      placement="bottom-start"
    >
      <template #reference>
        <div style="position: absolute;"></div>
      </template>
    </van-popover>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const showPopover = ref(false);
const actions = [
  { text: 'Copy' },
  { text: 'Paste' },
  { text: 'Delete' },
];

const showMenu = () => {
  showPopover.value = true;
};
</script>
```

## Best Practices

1. **Use appropriate placement**: Choose placement based on available space
2. **Limit actions**: Keep action list concise for better UX
3. **Provide visual feedback**: Use icons and colors for better recognition
4. **Consider mobile**: Ensure popover is accessible on touch devices
5. **Test positioning**: Verify popover positions correctly in different scenarios
