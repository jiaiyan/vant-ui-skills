---
name: "van-divider"
description: "Divider component for separating content into multiple areas. Invoke when user needs to create visual separators, section dividers, or content boundaries."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Divider Component

Separate content into multiple areas with customizable styles and content.

## When to Invoke

Invoke this skill when:
- User needs to separate content sections
- User wants to create visual dividers with text
- User needs horizontal or vertical separators
- User wants to customize divider style (dashed, solid)
- User asks about content positioning in dividers

## Features

- **Horizontal Dividers**: Standard horizontal separation
- **Vertical Dividers**: Vertical separation for inline content
- **Content Support**: Display text or content within the divider
- **Position Control**: Left, center, or right content positioning
- **Style Variants**: Solid or dashed lines
- **Hairline Support**: Ultra-thin lines for better visual effect
- **Custom Styling**: Full CSS customization support

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| dashed | Whether to use dashed border | `boolean` | `false` |
| hairline | Whether to use hairline | `boolean` | `true` |
| content-position | Content position, can be set to `left` `right` | `string` | `center` |
| vertical | Whether to use vertical | `boolean` | `false` |

### Slots

| Name | Description |
|------|-------------|
| default | Content |

### Types

```ts
import type { DividerProps, DividerContentPosition } from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-divider />
</template>
```

### With Text

```vue
<template>
  <van-divider>Text</van-divider>
</template>
```

### Content Position

```vue
<template>
  <van-divider content-position="left">Text</van-divider>
  <van-divider content-position="right">Text</van-divider>
</template>
```

### Dashed Style

```vue
<template>
  <van-divider dashed>Text</van-divider>
</template>
```

### Custom Style

```vue
<template>
  <van-divider
    :style="{ color: '#1989fa', borderColor: '#1989fa', padding: '0 16px' }"
  >
    Text
  </van-divider>
</template>
```

### Vertical Divider

```vue
<template>
  <van-divider vertical />
  Text
  <van-divider vertical dashed />
  Text
  <van-divider vertical :hairline="false" />
  Text
  <van-divider vertical :style="{ borderColor: '#1989fa' }" />
</template>
```

### With Icons

```vue
<template>
  <van-divider>
    <van-icon name="star-o" /> Favorites
  </van-divider>
</template>
```

### Section Separators

```vue
<template>
  <div class="section">
    <h3>Section 1</h3>
    <p>Content for section 1</p>
  </div>
  
  <van-divider>Section Divider</van-divider>
  
  <div class="section">
    <h3>Section 2</h3>
    <p>Content for section 2</p>
  </div>
</template>
```

## Common Issues

### 1. Divider Not Visible

Make sure there's enough space around the divider:

```vue
<div style="padding: 16px 0;">
  <van-divider />
</div>
```

### 2. Vertical Divider Height

Vertical dividers take the height of their container:

```vue
<div style="display: flex; align-items: center; height: 40px;">
  <span>Left</span>
  <van-divider vertical />
  <span>Right</span>
</div>
```

### 3. Custom Color Not Working

Use both `color` and `borderColor` for consistent styling:

```vue
<van-divider
  :style="{ 
    color: '#1989fa', 
    borderColor: '#1989fa' 
  }"
>
  Text
</van-divider>
```

## Component Interactions

### With Form Sections

```vue
<template>
  <van-form>
    <van-field v-model="username" label="Username" />
    <van-field v-model="email" label="Email" />
    
    <van-divider>Optional Information</van-divider>
    
    <van-field v-model="phone" label="Phone" />
    <van-field v-model="address" label="Address" />
  </van-form>
</template>
```

### With Card Layout

```vue
<template>
  <van-card>
    <template #title>
      Product Title
    </template>
    <template #desc>
      Product description
    </template>
  </van-card>
  
  <van-divider />
  
  <van-card>
    <template #title>
      Another Product
    </template>
  </van-card>
</template>
```

### In Navigation

```vue
<template>
  <van-space>
    <span>Home</span>
    <van-divider vertical />
    <span>Products</span>
    <van-divider vertical />
    <span>About</span>
  </van-space>
</template>
```

## Best Practices

1. **Use semantic meaning**: Add text to dividers to provide context
2. **Consistent styling**: Use consistent divider styles throughout the app
3. **Spacing**: Ensure adequate spacing around dividers for visual clarity
4. **Vertical dividers**: Use for inline separation, not for major sections
5. **Color contrast**: Ensure divider colors have sufficient contrast with background
