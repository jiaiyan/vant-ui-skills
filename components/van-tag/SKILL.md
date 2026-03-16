---
name: "van-tag"
description: "Tag component for marking keywords and labels. Invoke when user needs to display tags, labels, status indicators, or categorization badges."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Tag Component

Used to mark keywords and summarize the main content with various styles and types.

## When to Invoke

Invoke this skill when:
- User needs to display tags or labels
- User wants to show status indicators
- User needs to create categorization badges
- User asks about closable tags
- User wants to customize tag colors and styles

## Features

- **Multiple Types**: primary, success, danger, warning, default
- **Style Variants**: plain, round, mark styles
- **Custom Colors**: Custom background and text colors
- **Closable**: Optional close button with event
- **Size Options**: Default, medium, and large sizes
- **Show/Hide**: Toggle visibility

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| type | Type, can be set to `primary` `success` `danger` `warning` | `string` | `default` |
| size | Size, can be set to `large` `medium` | `string` | - |
| color | Custom color | `string` | - |
| show | Whether to show tag | `boolean` | `true` |
| plain | Whether to be plain style | `boolean` | `false` |
| round | Whether to be round style | `boolean` | `false` |
| mark | Whether to be mark style | `boolean` | `false` |
| text-color | Text color | `string` | `white` |
| closeable | Whether to be closeable | `boolean` | `false` |

### Slots

| Name | Description |
|------|-------------|
| default | Default slot for tag content |

### Events

| Name | Description | Arguments |
|------|-------------|-----------|
| click | Emitted when component is clicked | `event: MouseEvent` |
| close | Emitted when close icon is clicked | `event: MouseEvent` |

### Types

```ts
import type { TagSize, TagType, TagProps } from 'vant';
```

### CSS Variables

| Name | Default Value | Description |
|------|---------------|-------------|
| --van-tag-padding | `0 var(--van-padding-base)` | Tag padding |
| --van-tag-text-color | `var(--van-white)` | Text color |
| --van-tag-font-size | `var(--van-font-size-sm)` | Font size |
| --van-tag-radius | `2px` | Border radius |
| --van-tag-line-height | `16px` | Line height |
| --van-tag-medium-padding | `2px 6px` | Medium size padding |
| --van-tag-large-padding | `var(--van-padding-base) var(--van-padding-xs)` | Large size padding |
| --van-tag-large-radius | `var(--van-radius-md)` | Large size radius |
| --van-tag-large-font-size | `var(--van-font-size-md)` | Large size font |
| --van-tag-round-radius | `var(--van-radius-max)` | Round style radius |
| --van-tag-danger-color | `var(--van-danger-color)` | Danger color |
| --van-tag-primary-color | `var(--van-primary-color)` | Primary color |
| --van-tag-success-color | `var(--van-success-color)` | Success color |
| --van-tag-warning-color | `var(--van-warning-color)` | Warning color |
| --van-tag-default-color | `var(--van-gray-6)` | Default color |
| --van-tag-plain-background | `var(--van-background-2)` | Plain background |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-tag type="primary">Primary</van-tag>
  <van-tag type="success">Success</van-tag>
  <van-tag type="danger">Danger</van-tag>
  <van-tag type="warning">Warning</van-tag>
  <van-tag>Default</van-tag>
</template>
```

### Plain Style

```vue
<template>
  <van-tag plain type="primary">Primary</van-tag>
  <van-tag plain type="success">Success</van-tag>
  <van-tag plain type="danger">Danger</van-tag>
  <van-tag plain type="warning">Warning</van-tag>
</template>
```

### Round Style

```vue
<template>
  <van-tag round type="primary">Round Tag</van-tag>
  <van-tag round type="success">Success</van-tag>
  <van-tag round type="danger">Danger</van-tag>
</template>
```

### Mark Style

```vue
<template>
  <van-tag mark type="primary">Mark Tag</van-tag>
  <van-tag mark type="success">Success</van-tag>
  <van-tag mark type="danger">Danger</van-tag>
</template>
```

### Closeable

```vue
<template>
  <van-tag
    v-if="show"
    closeable
    size="medium"
    type="primary"
    @close="onClose"
  >
    Closeable Tag
  </van-tag>
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const show = ref(true);

const onClose = () => {
  show.value = false;
  showToast('Tag closed');
};
</script>
```

### Custom Size

```vue
<template>
  <van-tag type="primary">Default</van-tag>
  <van-tag type="primary" size="medium">Medium</van-tag>
  <van-tag type="primary" size="large">Large</van-tag>
</template>
```

### Custom Color

```vue
<template>
  <van-tag color="#7232dd">Custom Color</van-tag>
  <van-tag color="#ffe1e1" text-color="#ad0000">Custom Text</van-tag>
  <van-tag color="#7232dd" plain>Plain Custom</van-tag>
  <van-tag color="#7232dd" round>Round Custom</van-tag>
</template>
```

### Tag Group

```vue
<template>
  <div class="tag-group">
    <van-tag
      v-for="tag in tags"
      :key="tag.id"
      :type="tag.type"
      :plain="tag.plain"
      size="medium"
    >
      {{ tag.label }}
    </van-tag>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const tags = ref([
  { id: 1, label: 'Vue', type: 'primary', plain: false },
  { id: 2, label: 'React', type: 'success', plain: true },
  { id: 3, label: 'Angular', type: 'danger', plain: false },
  { id: 4, label: 'Svelte', type: 'warning', plain: true },
]);
</script>

<style>
.tag-group {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}
</style>
```

### Status Indicators

```vue
<template>
  <div class="status-list">
    <van-cell title="Order Status">
      <template #value>
        <van-tag :type="orderStatus.type">{{ orderStatus.text }}</van-tag>
      </template>
    </van-cell>
    <van-cell title="Payment Status">
      <template #value>
        <van-tag :type="paymentStatus.type">{{ paymentStatus.text }}</van-tag>
      </template>
    </van-cell>
    <van-cell title="Delivery Status">
      <template #value>
        <van-tag :type="deliveryStatus.type">{{ deliveryStatus.text }}</van-tag>
      </template>
    </van-cell>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const orderStatus = ref({ text: 'Processing', type: 'primary' });
const paymentStatus = ref({ text: 'Paid', type: 'success' });
const deliveryStatus = ref({ text: 'Pending', type: 'warning' });
</script>
```

### Selectable Tags

```vue
<template>
  <div class="selectable-tags">
    <van-tag
      v-for="tag in categories"
      :key="tag.id"
      :type="selectedTags.includes(tag.id) ? 'primary' : 'default'"
      :plain="!selectedTags.includes(tag.id)"
      size="medium"
      @click="toggleTag(tag.id)"
    >
      {{ tag.name }}
    </van-tag>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const categories = ref([
  { id: 1, name: 'Technology' },
  { id: 2, name: 'Design' },
  { id: 3, name: 'Business' },
  { id: 4, name: 'Marketing' },
]);

const selectedTags = ref([1, 3]);

const toggleTag = (id) => {
  const index = selectedTags.value.indexOf(id);
  if (index > -1) {
    selectedTags.value.splice(index, 1);
  } else {
    selectedTags.value.push(id);
  }
};
</script>

<style>
.selectable-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}
</style>
```

### Dynamic Tags

```vue
<template>
  <div class="dynamic-tags">
    <van-tag
      v-for="tag in dynamicTags"
      :key="tag"
      closeable
      size="medium"
      type="primary"
      @close="removeTag(tag)"
    >
      {{ tag }}
    </van-tag>
    <van-field
      v-model="newTag"
      placeholder="Add tag"
      @keyup.enter="addTag"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue';

const dynamicTags = ref(['Vue', 'React', 'Angular']);
const newTag = ref('');

const addTag = () => {
  if (newTag.value && !dynamicTags.value.includes(newTag.value)) {
    dynamicTags.value.push(newTag.value);
    newTag.value = '';
  }
};

const removeTag = (tag) => {
  const index = dynamicTags.value.indexOf(tag);
  if (index > -1) {
    dynamicTags.value.splice(index, 1);
  }
};
</script>

<style>
.dynamic-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  align-items: center;
}

.dynamic-tags .van-field {
  width: 100px;
}
</style>
```

### Product Labels

```vue
<template>
  <div class="product-card">
    <div class="product-image">
      <img src="product.jpg" alt="Product" />
      <div class="product-tags">
        <van-tag type="danger" mark>New</van-tag>
        <van-tag type="warning" mark>Sale</van-tag>
      </div>
    </div>
    <div class="product-info">
      <h4>Product Name</h4>
      <div class="price-tags">
        <van-tag type="danger" size="medium">$99.99</van-tag>
        <van-tag plain size="medium">$129.99</van-tag>
      </div>
    </div>
  </div>
</template>

<style>
.product-card {
  background: #fff;
  border-radius: 8px;
  overflow: hidden;
}

.product-image {
  position: relative;
}

.product-image img {
  width: 100%;
  height: 200px;
  object-fit: cover;
}

.product-tags {
  position: absolute;
  top: 8px;
  left: 8px;
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.product-info {
  padding: 12px;
}

.price-tags {
  display: flex;
  gap: 8px;
  margin-top: 8px;
}
</style>
```

## Best Practices

1. **Use semantic types**: Choose appropriate type based on content meaning
2. **Consistent sizing**: Use consistent sizes within the same context
3. **Plain for less emphasis**: Use plain style for less prominent tags
4. **Custom colors for branding**: Use custom colors to match brand identity
5. **Closable for user input**: Use closeable tags for user-added content
