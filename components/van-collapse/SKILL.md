---
name: "van-collapse"
description: "Collapse component for organizing content in expandable panels. Invoke when user needs to create accordion-style collapsible sections or FAQ lists."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Collapse Component

Place a group of content in multiple collapsible panels, click the title of the panel to expand or contract its content.

## When to Invoke

Invoke this skill when:
- User needs to create expandable/collapsible content sections
- User wants to implement accordion-style panels
- User needs to organize FAQ or Q&A content
- User wants to show/hide detailed information
- User asks about panel groups with single or multiple expansion

## Features

- **Accordion Mode**: Only one panel expanded at a time
- **Multiple Expansion**: Allow multiple panels open simultaneously
- **Disabled State**: Support disabled panels
- **Custom Titles**: Custom title slots with icons
- **Toggle All**: Method to toggle all panels at once
- **Lazy Render**: Lazy render content until opened
- **Border Control**: Customizable inner and outer borders

## API Reference

### Collapse Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model | Names of current active panels | accordion mode: `number \| string`<br>non-accordion mode: `(number \| string)[]` | - |
| accordion | Whether to be accordion mode | `boolean` | `false` |
| border | Whether to show outer border | `boolean` | `true` |

### Collapse Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| change | Emitted when switching panel | `activeNames: string \| number \| Array<string \| number>` |

### Collapse Methods

| Name | Description | Attribute | Return value |
|------|-------------|-----------|--------------|
| toggleAll | Toggle the expanded status of all collapses | `options?: boolean \| object` | - |

### CollapseItem Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| name | Name | `number \| string` | `index` |
| icon | Left Icon | `string` | - |
| size | Title size, can be set to `large` | `string` | - |
| title | Title | `number \| string` | - |
| value | Right text | `number \| string` | - |
| label | Description below the title | `string` | - |
| border | Whether to show inner border | `boolean` | `true` |
| disabled | Whether to disabled collapse | `boolean` | `false` |
| readonly | Whether to be readonly | `boolean` | `false` |
| is-link | Whether to show link icon | `boolean` | `true` |
| lazy-render | Whether to lazy render util opened | `boolean` | `true` |
| title-class | Title className | `string` | - |
| value-class | Value className | `string` | - |
| label-class | Label className | `string` | - |

### CollapseItem Methods

| Name | Description | Attribute | Return value |
|------|-------------|-----------|--------------|
| toggle | Toggle expanded status | `expanded: boolean` | - |

### CollapseItem Slots

| Name | Description |
|------|-------------|
| default | Content |
| title | Custom header title |
| value | Custom header value |
| label | Custom header label |
| icon | Custom header left icon |
| right-icon | Custom header right icon |

### Types

```ts
import type {
  CollapseProps,
  CollapseItemProps,
  CollapseItemInstance,
  CollapseToggleAllOptions,
} from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-collapse v-model="activeNames">
    <van-collapse-item title="Title1" name="1">
      The code is written for people to see and can be run on a machine.
    </van-collapse-item>
    <van-collapse-item title="Title2" name="2">
      Technology is nothing more than the common soul of those who develop it.
    </van-collapse-item>
    <van-collapse-item title="Title3" name="3">
      The frequency of people swearing during code reading is the only measure of code quality.
    </van-collapse-item>
  </van-collapse>
</template>

<script setup>
import { ref } from 'vue';

const activeNames = ref(['1']);
</script>
```

### Accordion Mode

```vue
<template>
  <van-collapse v-model="activeName" accordion>
    <van-collapse-item title="Title1" name="1">
      The code is written for people to see and can be run on a machine.
    </van-collapse-item>
    <van-collapse-item title="Title2" name="2">
      Technology is nothing more than the common soul of those who develop it.
    </van-collapse-item>
    <van-collapse-item title="Title3" name="3">
      The frequency of people swearing during code reading is the only measure of code quality.
    </van-collapse-item>
  </van-collapse>
</template>

<script setup>
import { ref } from 'vue';

const activeName = ref('1');
</script>
```

### Disabled State

```vue
<template>
  <van-collapse v-model="activeNames">
    <van-collapse-item title="Title1" name="1">
      Content 1
    </van-collapse-item>
    <van-collapse-item title="Title2" name="2" disabled>
      Content 2 - Disabled
    </van-collapse-item>
    <van-collapse-item title="Title3" name="3" disabled>
      Content 3 - Disabled
    </van-collapse-item>
  </van-collapse>
</template>
```

### Custom Title

```vue
<template>
  <van-collapse v-model="activeNames">
    <van-collapse-item name="1">
      <template #title>
        <div>Title1 <van-icon name="question-o" /></div>
      </template>
      Content 1
    </van-collapse-item>
    <van-collapse-item title="Title2" name="2" icon="shop-o">
      Content 2
    </van-collapse-item>
  </van-collapse>
</template>

<script setup>
import { ref } from 'vue';

const activeNames = ref(['1']);
</script>
```

### Toggle All

```vue
<template>
  <van-collapse v-model="activeNames" ref="collapse">
    <van-collapse-item title="Title1" name="1">
      Content 1
    </van-collapse-item>
    <van-collapse-item title="Title2" name="2">
      Content 2
    </van-collapse-item>
    <van-collapse-item title="Title3" name="3">
      Content 3
    </van-collapse-item>
  </van-collapse>

  <van-space style="margin-top: 16px;">
    <van-button type="primary" @click="openAll">Open All</van-button>
    <van-button type="primary" @click="toggleAll">Toggle All</van-button>
  </van-space>
</template>

<script setup>
import { ref } from 'vue';

const activeNames = ref(['1']);
const collapse = ref(null);

const openAll = () => {
  collapse.value.toggleAll(true);
};

const toggleAll = () => {
  collapse.value.toggleAll();
};
</script>
```

### Toggle All with Skip Disabled

```vue
<template>
  <van-collapse v-model="activeNames" ref="collapse">
    <van-collapse-item title="Title1" name="1">Content 1</van-collapse-item>
    <van-collapse-item title="Title2" name="2" disabled>Content 2</van-collapse-item>
    <van-collapse-item title="Title3" name="3">Content 3</van-collapse-item>
  </van-collapse>

  <van-button type="primary" @click="openAllSkipDisabled">
    Open All (Skip Disabled)
  </van-button>
</template>

<script setup>
import { ref } from 'vue';

const activeNames = ref(['1']);
const collapse = ref(null);

const openAllSkipDisabled = () => {
  collapse.value.toggleAll({
    expanded: true,
    skipDisabled: true,
  });
};
</script>
```

## Common Issues

### 1. toggleAll Not Working in Accordion Mode

The `toggleAll` method cannot be used in accordion mode. Use non-accordion mode instead:

```vue
<van-collapse v-model="activeNames">
  <!-- Non-accordion mode, toggleAll works -->
</van-collapse>
```

### 2. Content Not Rendering

If using `lazy-render` (default is true), content won't render until panel is opened. Disable it for SEO or initial content:

```vue
<van-collapse-item :lazy-render="false">
  Content will be rendered immediately
</van-collapse-item>
```

### 3. Programmatic Toggle

Use ref to get CollapseItem instance and toggle programmatically:

```vue
<template>
  <van-collapse v-model="activeNames">
    <van-collapse-item title="Title" name="1" ref="item">
      Content
    </van-collapse-item>
  </van-collapse>
  <van-button @click="toggleItem">Toggle Item</van-button>
</template>

<script setup>
import { ref } from 'vue';

const item = ref(null);

const toggleItem = () => {
  item.value.toggle();
};
</script>
```

## Component Interactions

### With Cell Component

```vue
<template>
  <van-collapse v-model="activeNames">
    <van-collapse-item title="User Info" name="user">
      <van-cell-group>
        <van-cell title="Name" value="John" />
        <van-cell title="Email" value="john@example.com" />
        <van-cell title="Phone" value="123-456-7890" />
      </van-cell-group>
    </van-collapse-item>
  </van-collapse>
</template>
```

### FAQ Section

```vue
<template>
  <van-collapse v-model="activeNames" accordion>
    <van-collapse-item
      v-for="faq in faqList"
      :key="faq.id"
      :title="faq.question"
      :name="faq.id"
    >
      {{ faq.answer }}
    </van-collapse-item>
  </van-collapse>
</template>

<script setup>
import { ref } from 'vue';

const activeNames = ref('');
const faqList = ref([
  { id: '1', question: 'How to use?', answer: 'Click to expand...' },
  { id: '2', question: 'Is it free?', answer: 'Yes, it is free...' },
]);
</script>
```

## Best Practices

1. **Use accordion for single selection**: Use accordion mode when only one panel should be open
2. **Provide meaningful names**: Use descriptive names for each panel for easier management
3. **Lazy render for performance**: Keep lazy-render enabled for better performance with large content
4. **Visual feedback**: Use icons and labels to indicate expandable content
5. **Accessibility**: Ensure titles are descriptive for screen readers
