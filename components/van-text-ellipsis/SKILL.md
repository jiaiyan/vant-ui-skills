---
name: "van-text-ellipsis"
description: "Text ellipsis component for truncating long text with expand/collapse support. Invoke when user needs to display truncated text with expand/collapse functionality."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant TextEllipsis Component

Display ellipsis for long text and support for expanding or collapsing text content.

## When to Invoke

Invoke this skill when:
- User needs to truncate long text with ellipsis
- User wants to add expand/collapse functionality to text
- User needs to limit text to specific number of rows
- User asks about text overflow handling
- User wants to customize ellipsis position

## Features

- **Row Limit**: Display specified number of rows
- **Expand/Collapse**: Toggle between truncated and full text
- **Custom Position**: Ellipsis at end, start, or middle
- **Custom Dots**: Customizable ellipsis text
- **Custom Actions**: Custom expand/collapse buttons
- **Programmatic Control**: Toggle method for manual control

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| rows | Number of rows displayed | `number \| string` | `1` |
| content | The text displayed | `string` | - |
| expand-text | Expand operation text | `string` | - |
| collapse-text | Collapse operation text | `string` | - |
| dots | Text content of ellipsis | `string` | `'...'` |
| position | Can be set to `start` `middle` | `string` | `'end'` |

### Events

| Name | Description | Arguments |
|------|-------------|-----------|
| click-action | Emitted when Expand/Collapse is clicked | `event: MouseEvent` |

### Methods

Use ref to get TextEllipsis instance and call instance methods.

| Name | Description | Arguments | Return Value |
|------|-------------|-----------|--------------|
| toggle | Toggle expanded status | `expanded?: boolean` | - |

### Slots

| Name | Description | SlotProps |
|------|-------------|-----------|
| action | Custom action | `{ expanded: boolean }` |

### Types

```ts
import type {
  TextEllipsisProps,
  TextEllipsisInstance,
  TextEllipsisThemeVars,
} from 'vant';
```

### CSS Variables

| Name | Default Value | Description |
|------|---------------|-------------|
| --van-text-ellipsis-action-color | `var(--van-blue)` | Color of action text |
| --van-text-ellipsis-line-height | `1.6` | Line height of text |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-text-ellipsis :content="text" />
</template>

<script setup>
const text = 'Take your time and be patient. Life itself will eventually answer all those questions it once raised for you.';
</script>
```

### Expand/Collapse

```vue
<template>
  <van-text-ellipsis
    :content="text"
    expand-text="Expand"
    collapse-text="Collapse"
  />
</template>

<script setup>
const text = "The fleeting time of one's life is everything that belongs to a person. Only this thing truly belongs to you. Everything else is just a momentary pleasure or misfortune, which will soon be gone with the passing of time.";
</script>
```

### Customize Rows

```vue
<template>
  <van-text-ellipsis
    rows="3"
    :content="text"
    expand-text="Expand"
    collapse-text="Collapse"
  />
</template>

<script setup>
const text = "That day, I turned twenty-one. In the golden age of my life, I was full of dreams. I wanted to love, to eat, and to instantly transform into one of these clouds, part alight, part darkened. It was only later that I understood life is but a slow, drawn-out process of getting your balls crushed. Day by day, you get older. Day by day, your dreams fade. In the end you are no different from a crushed ox. But I hadn't foreseen any of it on my twenty-first birthday. I thought I would be vigorous forever, and that nothing could ever crush me.";
</script>
```

### Collapse at Start

```vue
<template>
  <van-text-ellipsis
    rows="1"
    :content="text"
    expand-text="Expand"
    collapse-text="Collapse"
    position="start"
  />
</template>

<script setup>
const text = "That day, I turned twenty-one. In the golden age of my life, I was full of dreams. I wanted to love, to eat, and to instantly transform into one of these clouds.";
</script>
```

### Collapse at Middle

```vue
<template>
  <van-text-ellipsis
    rows="2"
    :content="text"
    expand-text="Expand"
    collapse-text="Collapse"
    position="middle"
  />
</template>

<script setup>
const text = "That day, I turned twenty-one. In the golden age of my life, I was full of dreams. I wanted to love, to eat, and to instantly transform into one of these clouds, part alight, part darkened.";
</script>
```

### Custom Action

```vue
<template>
  <van-text-ellipsis :content="text">
    <template #action="{ expanded }">
      {{ expanded ? 'Show Less' : 'Show More' }}
    </template>
  </van-text-ellipsis>
</template>

<script setup>
const text = 'Take your time and be patient. Life itself will eventually answer all those questions it once raised for you.';
</script>
```

### Custom Dots

```vue
<template>
  <van-text-ellipsis
    :content="text"
    dots="……"
    expand-text="Read More"
    collapse-text="Read Less"
  />
</template>

<script setup>
const text = 'Take your time and be patient. Life itself will eventually answer all those questions it once raised for you.';
</script>
```

### Manual Control

```vue
<template>
  <div>
    <van-text-ellipsis
      ref="ellipsisRef"
      :content="text"
      expand-text="Expand"
      collapse-text="Collapse"
    />
    <div class="controls">
      <van-button size="small" @click="expand">Expand</van-button>
      <van-button size="small" @click="collapse">Collapse</van-button>
      <van-button size="small" @click="toggle">Toggle</van-button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const ellipsisRef = ref(null);
const text = 'Take your time and be patient. Life itself will eventually answer all those questions it once raised for you.';

const expand = () => {
  ellipsisRef.value?.toggle(true);
};

const collapse = () => {
  ellipsisRef.value?.toggle(false);
};

const toggle = () => {
  ellipsisRef.value?.toggle();
};
</script>

<style>
.controls {
  margin-top: 12px;
  display: flex;
  gap: 8px;
}
</style>
```

### Product Description

```vue
<template>
  <div class="product-card">
    <h3>Product Name</h3>
    <van-text-ellipsis
      rows="2"
      :content="description"
      expand-text="Read more"
      collapse-text="Show less"
    />
    <div class="price">$99.99</div>
  </div>
</template>

<script setup>
const description = 'This is a high-quality product with excellent features. It is designed to meet all your needs and provide the best user experience. The product comes with a warranty and customer support.';
</script>

<style>
.product-card {
  padding: 16px;
  background: #fff;
  border-radius: 8px;
}

.price {
  margin-top: 12px;
  font-size: 18px;
  font-weight: bold;
  color: #f44;
}
</style>
```

### Article Preview

```vue
<template>
  <div class="article-list">
    <div v-for="article in articles" :key="article.id" class="article-item">
      <h4>{{ article.title }}</h4>
      <van-text-ellipsis
        rows="3"
        :content="article.content"
        expand-text="Read full article"
        collapse-text="Collapse"
      />
      <div class="meta">
        <span>{{ article.date }}</span>
        <span>{{ article.author }}</span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const articles = ref([
  {
    id: 1,
    title: 'Understanding Vue 3 Composition API',
    content: 'The Composition API is a set of APIs that allow flexible composition of component logic. It provides a way to organize and reuse code that is more flexible than the Options API. With the Composition API, you can group related logic together and extract it into composable functions.',
    date: '2024-01-15',
    author: 'John Doe',
  },
  {
    id: 2,
    title: 'Best Practices for Mobile Development',
    content: 'Mobile development requires careful consideration of performance, user experience, and platform-specific guidelines. This article covers the essential best practices every mobile developer should know, from responsive design to efficient data handling.',
    date: '2024-01-14',
    author: 'Jane Smith',
  },
]);
</script>

<style>
.article-list {
  background: #f7f8fa;
}

.article-item {
  padding: 16px;
  background: #fff;
  margin-bottom: 12px;
}

.article-item h4 {
  margin: 0 0 8px;
}

.meta {
  margin-top: 12px;
  display: flex;
  gap: 16px;
  font-size: 12px;
  color: #969799;
}
</style>
```

### Comment Section

```vue
<template>
  <div class="comment-section">
    <div v-for="comment in comments" :key="comment.id" class="comment-item">
      <div class="comment-header">
        <img :src="comment.avatar" class="avatar" />
        <div class="user-info">
          <span class="username">{{ comment.username }}</span>
          <span class="time">{{ comment.time }}</span>
        </div>
      </div>
      <van-text-ellipsis
        rows="3"
        :content="comment.content"
        expand-text="Expand"
        collapse-text="Collapse"
      />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const comments = ref([
  {
    id: 1,
    username: 'User A',
    avatar: 'https://fastly.jsdelivr.net/npm/@vant/assets/cat.jpeg',
    time: '2 hours ago',
    content: 'This is a great product! I have been using it for a while and it has exceeded my expectations. The quality is excellent and the customer service is very responsive. I would definitely recommend this to anyone looking for a reliable solution.',
  },
  {
    id: 2,
    username: 'User B',
    avatar: 'https://fastly.jsdelivr.net/npm/@vant/assets/cat.jpeg',
    time: '5 hours ago',
    content: 'Good value for money. The shipping was fast and the product arrived in perfect condition.',
  },
]);
</script>

<style>
.comment-section {
  background: #fff;
}

.comment-item {
  padding: 16px;
  border-bottom: 1px solid #ebedf0;
}

.comment-header {
  display: flex;
  align-items: center;
  margin-bottom: 12px;
}

.avatar {
  width: 32px;
  height: 32px;
  border-radius: 50%;
  margin-right: 12px;
}

.user-info {
  display: flex;
  flex-direction: column;
}

.username {
  font-weight: 500;
}

.time {
  font-size: 12px;
  color: #969799;
}
</style>
```

## Best Practices

1. **Set appropriate rows**: Choose row count based on content importance
2. **Use clear action text**: Make expand/collapse text intuitive
3. **Consider position**: Use `start` or `middle` position for specific use cases
4. **Custom actions for branding**: Use custom action slots for consistent styling
5. **Handle long content**: Always provide expand option for important content
