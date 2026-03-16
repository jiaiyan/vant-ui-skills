---
name: "van-style"
description: "Built-in style utilities for common CSS patterns. Invoke when user needs text ellipsis, hairlines, safe areas, animations, or clearfix."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Built-in Styles

Vant contains some common styles that can be used directly by the className.

## When to Invoke

Invoke this skill when:
- User needs text truncation or ellipsis
- User wants to add 1px borders (hairlines)
- User needs to handle safe area for iOS devices
- User wants to use built-in animations
- User needs clearfix for floated elements
- User wants haptic feedback styles

## Features

- **Text Ellipsis**: Single and multi-line text truncation
- **Hairline**: 1px borders for Retina screens
- **Safe Area**: iOS safe area adaptation
- **Animations**: Fade, slide, and other transitions
- **Haptic Feedback**: Touch feedback styles
- **Clearfix**: Clear floated content

## Text Ellipsis

### Single Line Ellipsis

When the text content length exceeds the maximum container width, the excess text is automatically omitted.

```vue
<template>
  <div class="van-ellipsis">
    This is a paragraph that displays up to one line of text, and the rest of the
    text will be omitted.
  </div>
</template>
```

### Multi-line Ellipsis

```vue
<template>
  <div class="van-multi-ellipsis--l2">
    This is a paragraph that displays up to two lines of text, and the rest of the
    text will be omitted.
  </div>

  <div class="van-multi-ellipsis--l3">
    This is a paragraph that displays up to three lines of text, and the rest of
    the text will be omitted.
  </div>
</template>
```

## Hairline

Add 1px border under the Retina screen for the element, based on a pseudo element.

### Single Direction

```vue
<template>
  <div class="van-hairline--top">Border Top</div>
  <div class="van-hairline--bottom">Border Bottom</div>
  <div class="van-hairline--left">Border Left</div>
  <div class="van-hairline--right">Border Right</div>
</template>
```

### Multiple Directions

```vue
<template>
  <div class="van-hairline--top-bottom">Border Top & Bottom</div>
  <div class="van-hairline--surround">Full Border</div>
</template>
```

### Custom Styling

```vue
<template>
  <div class="card van-hairline--surround">
    Card with hairline border
  </div>
</template>

<style scoped>
.card {
  padding: 16px;
  border-radius: 8px;
}

:deep(.van-hairline--surround::after) {
  border-color: #eee;
}
</style>
```

## Safe Area

Enable safe area for iOS devices with notch or home indicator.

### Top Safe Area

```vue
<template>
  <div class="van-safe-area-top">
    Content with top safe area padding
  </div>
</template>
```

### Bottom Safe Area

```vue
<template>
  <div class="van-safe-area-bottom">
    Content with bottom safe area padding
  </div>
</template>
```

### Fixed Bottom Bar

```vue
<template>
  <div class="fixed-bottom van-hairline--top van-safe-area-bottom">
    <van-button type="primary" block>Submit</van-button>
  </div>
</template>

<style scoped>
.fixed-bottom {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 12px 16px;
  background: #fff;
}
</style>
```

## Animations

### Fade

```vue
<template>
  <transition name="van-fade">
    <div v-show="visible" class="box">Fade Animation</div>
  </transition>
</template>

<script setup>
import { ref } from 'vue';

const visible = ref(true);
</script>
```

### Slide Up

```vue
<template>
  <transition name="van-slide-up">
    <div v-show="visible" class="box">Slide Up</div>
  </transition>
</template>
```

### Slide Down

```vue
<template>
  <transition name="van-slide-down">
    <div v-show="visible" class="box">Slide Down</div>
  </transition>
</template>
```

### Slide Left

```vue
<template>
  <transition name="van-slide-left">
    <div v-show="visible" class="box">Slide Left</div>
  </transition>
</template>
```

### Slide Right

```vue
<template>
  <transition name="van-slide-right">
    <div v-show="visible" class="box">Slide Right</div>
  </transition>
</template>
```

### Complete Animation Example

```vue
<template>
  <div>
    <van-button @click="visible = !visible">Toggle</van-button>
    
    <transition name="van-fade">
      <div v-if="visible" class="box">Fade Content</div>
    </transition>
    
    <transition name="van-slide-up">
      <div v-if="visible" class="box">Slide Up Content</div>
    </transition>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const visible = ref(false);
</script>

<style scoped>
.box {
  margin-top: 16px;
  padding: 20px;
  background: #f5f5f5;
  border-radius: 8px;
}
</style>
```

## Haptic Feedback

Add haptic feedback for an element. When touched, the opacity of the element is reduced.

```vue
<template>
  <div class="van-haptics-feedback clickable-item">
    Click me for haptic feedback
  </div>
</template>

<style scoped>
.clickable-item {
  padding: 16px;
  background: #fff;
  cursor: pointer;
}
</style>
```

### With Button

```vue
<template>
  <div class="custom-button van-haptics-feedback">
    Custom Button
  </div>
</template>

<style scoped>
.custom-button {
  display: inline-block;
  padding: 8px 16px;
  background: #1989fa;
  color: #fff;
  border-radius: 4px;
  cursor: pointer;
}
</style>
```

## Clearfix

Clear floated content within a container.

```vue
<template>
  <div class="van-clearfix">
    <div class="float-left">Left</div>
    <div class="float-right">Right</div>
  </div>
</template>

<style scoped>
.float-left {
  float: left;
}

.float-right {
  float: right;
}
</style>
```

## Combined Usage

### Card with Ellipsis and Hairline

```vue
<template>
  <div class="card van-hairline--surround">
    <h3 class="van-ellipsis">This is a very long title that will be truncated</h3>
    <p class="van-multi-ellipsis--l2">
      This is a description that can span multiple lines and will be truncated
      after two lines of text.
    </p>
  </div>
</template>

<style scoped>
.card {
  padding: 16px;
  border-radius: 8px;
  background: #fff;
}

.card h3 {
  margin-bottom: 8px;
}

.card p {
  color: #666;
}
</style>
```

### Modal with Animations and Safe Area

```vue
<template>
  <transition name="van-fade">
    <div v-if="visible" class="modal-overlay">
      <transition name="van-slide-up">
        <div v-if="visible" class="modal-content van-safe-area-bottom">
          <div class="van-hairline--bottom modal-header">
            <h3>Modal Title</h3>
          </div>
          <div class="modal-body">
            <p class="van-multi-ellipsis--l3">
              Modal content goes here. This text will be truncated after three lines.
            </p>
          </div>
          <div class="van-hairline--top modal-footer">
            <van-button block type="primary" @click="visible = false">
              Close
            </van-button>
          </div>
        </div>
      </transition>
    </div>
  </transition>
</template>

<script setup>
import { ref } from 'vue';

const visible = ref(false);
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: flex-end;
}

.modal-content {
  width: 100%;
  background: #fff;
  border-radius: 16px 16px 0 0;
}

.modal-header {
  padding: 16px;
  text-align: center;
}

.modal-body {
  padding: 16px;
}

.modal-footer {
  padding: 12px 16px;
}
</style>
```

## Best Practices

1. **Use ellipsis for long text**: Prevent layout issues with text overflow
2. **Hairlines for borders**: Use hairlines for crisp 1px borders on Retina screens
3. **Safe area for iOS**: Always add safe area for fixed bottom elements
4. **Animations**: Use built-in transitions for consistent UI feel
5. **Haptic feedback**: Add to clickable elements for better mobile experience
