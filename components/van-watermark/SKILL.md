---
name: "van-watermark"
description: "Watermark component for adding text or image watermarks to pages. Invoke when user needs to add watermarks for copyright protection or information security."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Watermark Component

Add specific text or patterns on the page as watermarks, which can be used to prevent information theft.

## When to Invoke

Invoke this skill when:
- User needs to add text watermarks to pages
- User wants to add image watermarks
- User needs to protect content from unauthorized copying
- User asks about watermark customization
- User wants to create full-page or container watermarks

## Features

- **Text Watermark**: Display text as watermark
- **Image Watermark**: Display image as watermark
- **HTML Watermark**: Custom HTML content as watermark
- **Custom Gap**: Control horizontal and vertical spacing
- **Rotation Control**: Customizable watermark rotation angle
- **Full Page Mode**: Display watermark across entire page
- **Opacity Control**: Adjust watermark transparency

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| width | Watermark width | `number` | `100` |
| height | Watermark height | `number` | `100` |
| z-index | Watermark's z-index | `number \| string` | `100` |
| content | Text watermark content | `string` | - |
| image | Image watermark content. If `content` and `image` are passed at the same time, use the `image` watermark first | `string` | - |
| rotate | Watermark rotation angle | `number \| string` | `-22` |
| full-page | Whether to display the watermark in full screen | `boolean` | `true` |
| gap-x | Horizontal spacing between watermarks | `number` | `0` |
| gap-y | Vertical spacing between watermarks | `number` | `0` |
| text-color | Color of text watermark | `string` | `#dcdee0` |
| opacity | Opacity of watermark | `number \| string` | - |

### Slots

| Name | Description |
|------|-------------|
| content | Content of HTML watermark. Only supports inline styles, and self-closing tags are not supported. The priority is higher than `content` or `image` props |

### Types

```ts
import type { WaterProps } from 'vant';
```

### CSS Variables

| Name | Default Value | Description |
|------|---------------|-------------|
| --van-watermark-z-index | `100` | z-index of root element |

## Usage Examples

### Text Watermark

```vue
<template>
  <van-watermark content="Vant" />
</template>
```

### Image Watermark

```vue
<template>
  <van-watermark
    image="https://fastly.jsdelivr.net/npm/@vant/assets/vant-watermark.png"
    opacity="0.2"
  />
</template>
```

### Custom Gap

```vue
<template>
  <van-watermark
    image="https://fastly.jsdelivr.net/npm/@vant/assets/vant-watermark.png"
    :gap-x="30"
    :gap-y="10"
    opacity="0.2"
  />
</template>
```

### Custom Rotate

```vue
<template>
  <van-watermark
    image="https://fastly.jsdelivr.net/npm/@vant/assets/vant-watermark.png"
    rotate="22"
    opacity="0.2"
  />
</template>
```

### Display Range

```vue
<template>
  <van-watermark
    image="https://fastly.jsdelivr.net/npm/@vant/assets/vant-watermark.png"
    opacity="0.2"
    :full-page="true"
  />
</template>
```

### HTML Watermark

```vue
<template>
  <van-watermark :width="150">
    <template #content>
      <div style="background: linear-gradient(45deg, #000 0, #000 50%, #fff 50%)">
        <p style="mix-blend-mode: difference; color: #fff">Vant watermark</p>
      </div>
    </template>
  </van-watermark>
</template>
```

### Container Watermark

```vue
<template>
  <div class="container">
    <van-watermark
      content="Confidential"
      :full-page="false"
      opacity="0.15"
    />
    <div class="content">
      <h3>Confidential Document</h3>
      <p>This is a confidential document with watermark protection.</p>
      <p>The watermark is only visible within this container.</p>
    </div>
  </div>
</template>

<style>
.container {
  position: relative;
  height: 300px;
  overflow: hidden;
  background: #fff;
  border: 1px solid #ebedf0;
  border-radius: 8px;
}

.content {
  position: relative;
  z-index: 1;
  padding: 20px;
}
</style>
```

### Multi-line Text Watermark

```vue
<template>
  <van-watermark :width="200" :height="80">
    <template #content>
      <div style="font-size: 12px; color: #999; text-align: center;">
        <div>Company Name</div>
        <div>Confidential</div>
      </div>
    </template>
  </van-watermark>
</template>
```

### Document Protection

```vue
<template>
  <div class="document-page">
    <van-watermark
      :content="watermarkText"
      text-color="rgba(0, 0, 0, 0.1)"
      :gap-x="100"
      :gap-y="50"
      rotate="-30"
    />
    <div class="document-content">
      <h1>Important Document</h1>
      <p>This document contains sensitive information.</p>
      <p>Watermark helps protect against unauthorized copying.</p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const watermarkText = ref('CONFIDENTIAL - DO NOT COPY');
</script>

<style>
.document-page {
  position: relative;
  min-height: 100vh;
  background: #fff;
}

.document-content {
  position: relative;
  z-index: 1;
  padding: 24px;
  max-width: 800px;
  margin: 0 auto;
}
</style>
```

### User-Specific Watermark

```vue
<template>
  <van-watermark
    :content="userWatermark"
    :opacity="0.1"
    :gap-x="150"
    :gap-y="100"
  />
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  username: String,
  userId: String,
});

const userWatermark = computed(() => {
  return `${props.username} - ${props.userId}`;
});
</script>
```

### Preview Protection

```vue
<template>
  <div class="preview-container">
    <van-watermark
      image="https://fastly.jsdelivr.net/npm/@vant/assets/vant-watermark.png"
      :opacity="0.3"
      :full-page="false"
    />
    <img :src="previewImage" class="preview-image" />
  </div>
</template>

<script setup>
import { ref } from 'vue';

const previewImage = ref('https://fastly.jsdelivr.net/npm/@vant/assets/apple-1.jpeg');
</script>

<style>
.preview-container {
  position: relative;
  display: inline-block;
}

.preview-image {
  display: block;
  max-width: 100%;
}
</style>
```

### Dynamic Watermark

```vue
<template>
  <div>
    <van-watermark
      :content="watermarkContent"
      :opacity="watermarkOpacity"
      :rotate="watermarkRotate"
    />
    
    <div class="controls">
      <van-field v-model="watermarkContent" label="Content" />
      <van-field v-model="watermarkOpacity" label="Opacity" type="number" />
      <van-slider v-model="watermarkRotate" :min="-90" :max="90" />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const watermarkContent = ref('Vant');
const watermarkOpacity = ref(0.2);
const watermarkRotate = ref(-22);
</script>

<style>
.controls {
  position: fixed;
  bottom: 20px;
  left: 20px;
  right: 20px;
  background: #fff;
  padding: 16px;
  border-radius: 8px;
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.1);
  z-index: 1000;
}
</style>
```

### Conditional Watermark

```vue
<template>
  <van-watermark
    v-if="showWatermark"
    :content="watermarkText"
    :opacity="0.15"
  />
  <div class="content">
    <van-switch v-model="showWatermark" />
    <span>Show Watermark</span>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const showWatermark = ref(true);
const watermarkText = ref('DRAFT');
</script>
```

## Best Practices

1. **Use appropriate opacity**: Set opacity low enough to not interfere with content
2. **Full page for protection**: Use `full-page="true"` for content protection
3. **User-specific watermarks**: Include user info for traceability
4. **Consistent styling**: Match watermark style with brand identity
5. **Performance consideration**: Use image watermarks for complex designs
