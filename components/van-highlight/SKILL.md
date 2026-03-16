---
name: "van-highlight"
description: "Highlight component for emphasizing specific text content. Invoke when user needs to highlight keywords in text or implement search result highlighting."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Highlight Component

Highlight the specified text content within a larger text block.

## When to Invoke

Invoke this skill when:
- User needs to highlight specific keywords in text
- User wants to implement search result highlighting
- User needs to emphasize certain words or phrases
- User wants to customize highlight styles
- User asks about case-sensitive or case-insensitive highlighting

## Features

- **Single/Multiple Keywords**: Support single or multiple keyword highlighting
- **Case Sensitivity**: Configurable case-sensitive matching
- **Auto Escape**: Automatic special character escaping
- **Custom Styling**: Custom CSS classes for highlighted text
- **Custom Tags**: Configurable HTML tags for highlighted elements
- **Flexible Configuration**: Multiple customization options

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| auto-escape | Whether to automatically escape | `boolean` | `true` |
| case-sensitive | Is case sensitive | `boolean` | `false` |
| highlight-class | Class name of the highlight element | `string` | - |
| highlight-tag | HTML Tag of highlighted element | `string` | `span` |
| keywords | Expected highlighted text | `string \| string[]` | - |
| source-string | Source text | `string` | - |
| tag | HTML Tag of root element | `string` | `div` |
| unhighlight-class | Class name of the unhighlight element | `string` | - |
| unhighlight-tag | HTML Tag of unhighlighted element | `string` | `span` |

### Types

```ts
import type { HighlightProps, HighlightThemeVars } from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-highlight :keywords="keywords" :source-string="text" />
</template>

<script setup>
import { ref } from 'vue';

const text = 'Take your time and be patient. Life itself will eventually answer all those questions it once raised for you.';
const keywords = 'questions';
</script>
```

### Multiple Keywords

```vue
<template>
  <van-highlight :keywords="keywords" :source-string="text" />
</template>

<script setup>
import { ref } from 'vue';

const text = 'Take your time and be patient. Life itself will eventually answer all those questions it once raised for you.';
const keywords = ['time', 'life', 'answer'];
</script>
```

### Custom Class

```vue
<template>
  <van-highlight
    :keywords="keywords"
    :source-string="text"
    highlight-class="custom-highlight"
  />
</template>

<script setup>
import { ref } from 'vue';

const text = 'Take your time and be patient. Life itself will eventually answer all those questions it once raised for you.';
const keywords = 'life';
</script>

<style scoped>
.custom-highlight {
  color: red;
  font-weight: bold;
}
</style>
```

### Case Sensitive

```vue
<template>
  <van-highlight
    :keywords="keywords"
    :source-string="text"
    :case-sensitive="true"
  />
</template>

<script setup>
import { ref } from 'vue';

const text = 'Life is beautiful. life is precious.';
const keywords = 'Life';
</script>
```

### Custom Tags

```vue
<template>
  <van-highlight
    :keywords="keywords"
    :source-string="text"
    highlight-tag="mark"
    tag="p"
  />
</template>

<script setup>
import { ref } from 'vue';

const text = 'This is important text';
const keywords = 'important';
</script>
```

### With Search Input

```vue
<template>
  <van-search v-model="searchText" placeholder="Search..." />
  <van-highlight
    :keywords="searchText"
    :source-string="content"
  />
</template>

<script setup>
import { ref } from 'vue';

const searchText = ref('');
const content = 'This is a long text that can be searched and highlighted based on user input.';
</script>
```

## Common Issues

### 1. Special Characters Not Matching

Enable `auto-escape` to handle special regex characters:

```vue
<van-highlight
  :keywords="keywords"
  :source-string="text"
  :auto-escape="true"
/>
```

### 2. Case Sensitivity Issues

By default, highlighting is case-insensitive. Enable case-sensitive for exact matching:

```vue
<van-highlight
  :keywords="keywords"
  :source-string="text"
  :case-sensitive="true"
/>
```

### 3. Styling Not Applied

Make sure to use the correct class name:

```vue
<van-highlight
  :keywords="keywords"
  :source-string="text"
  highlight-class="my-highlight"
/>

<style>
.my-highlight {
  background-color: yellow;
}
</style>
```

## Component Interactions

### With Search Results

```vue
<template>
  <van-search v-model="keyword" placeholder="Search..." />
  <van-list>
    <van-cell v-for="result in results" :key="result.id">
      <van-highlight
        :keywords="keyword"
        :source-string="result.title"
      />
    </van-cell>
  </van-list>
</template>

<script setup>
import { ref } from 'vue';

const keyword = ref('');
const results = ref([
  { id: 1, title: 'Introduction to Vue.js' },
  { id: 2, title: 'Advanced Vue.js Patterns' },
]);
</script>
```

### With Dynamic Content

```vue
<template>
  <van-field v-model="inputText" label="Text" />
  <van-field v-model="keyword" label="Keyword" />
  <van-highlight
    :keywords="keyword"
    :source-string="inputText"
    highlight-class="highlight-text"
  />
</template>

<script setup>
import { ref } from 'vue';

const inputText = ref('Type something here');
const keyword = ref('');
</script>

<style>
.highlight-text {
  background-color: #ffeb3b;
  padding: 0 2px;
  border-radius: 2px;
}
</style>
```

### With List Filter

```vue
<template>
  <van-search v-model="searchValue" placeholder="Filter items" />
  <van-cell-group>
    <van-cell v-for="item in filteredItems" :key="item.id">
      <van-highlight
        :keywords="searchValue"
        :source-string="item.name"
      />
    </van-cell>
  </van-cell-group>
</template>

<script setup>
import { ref, computed } from 'vue';

const searchValue = ref('');
const items = ref([
  { id: 1, name: 'Apple' },
  { id: 2, name: 'Banana' },
  { id: 3, name: 'Orange' },
]);

const filteredItems = computed(() => {
  if (!searchValue.value) return items.value;
  return items.value.filter(item =>
    item.name.toLowerCase().includes(searchValue.value.toLowerCase())
  );
});
</script>
```

## Best Practices

1. **Use auto-escape**: Always enable auto-escape when dealing with user input
2. **Performance**: For large texts, consider debouncing search input
3. **Accessibility**: Ensure highlighted text has sufficient contrast
4. **Consistent styling**: Use consistent highlight styles across the app
5. **Multiple keywords**: Use array for multiple keywords when needed
