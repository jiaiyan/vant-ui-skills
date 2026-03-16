---
name: "vant-advanced-usage"
description: "Covers advanced Vant usage patterns including component registration, browser adaptation, and performance optimization. Invoke when user needs advanced configuration or encounters complex scenarios."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Advanced Usage

This skill provides comprehensive guidance for advanced Vant usage patterns, including component registration methods, browser adaptation strategies, and performance optimization techniques.

## When to Invoke

Invoke this skill when:
- User needs different component registration methods
- User wants to adapt Vant for different screen sizes
- User needs to use Vant on PC browsers
- User asks about viewport units (vw/vh) or rem units
- User needs performance optimization tips

## Component Registration

### Global Registration

Register components globally using `app.use`:

```js
import { Button } from 'vant';
import { createApp } from 'vue';

const app = createApp();

// Method 1: via app.use
app.use(Button);

// Method 2: via app.component
app.component(Button.name, Button);
```

### Full Registration

Register all Vant components at once:

```js
import Vant from 'vant';
import { createApp } from 'vue';

const app = createApp();

app.use(Vant);

// The Lazyload directive needs to be registered separately
app.use(vant.Lazyload);
```

> **Warning**: Registering all components will introduce the code of all components, leading to larger bundle size.

### Local Registration

Register components locally in Vue components:

```js
import { Button } from 'vant';

export default {
  components: {
    [Button.name]: Button,
  },
};
```

### Script Setup

Vant components can be used directly in `<script setup>` without registration:

```vue
<script setup>
import { Button } from 'vant';
</script>

<template>
  <Button />
</template>
```

### JSX/TSX

Vant components can be used directly in JSX and TSX:

```jsx
import { Button } from 'vant';

export default {
  render() {
    return <Button />;
  },
};
```

## Browser Adaptation

### Viewport Units (vw/vh)

Vant uses `px` unit by default. Use [postcss-px-to-viewport](https://github.com/evrone/postcss-px-to-viewport) to transform `px` to viewport units:

```js
// postcss.config.js
module.exports = {
  plugins: {
    'postcss-px-to-viewport': {
      viewportWidth: 375,
    },
  },
};
```

### Rem Units

Use `postcss-pxtorem` to transform `px` to `rem`:

```js
// postcss.config.js
module.exports = {
  plugins: {
    'postcss-pxtorem': {
      rootValue: 37.5,
      propList: ['*'],
    },
  },
};
```

### Custom rootValue for Different Design Sizes

For 750px or other design sizes:

```js
// postcss.config.js
module.exports = {
  plugins: {
    'postcss-pxtorem': {
      rootValue({ file }) {
        return file.indexOf('vant') !== -1 ? 37.5 : 75;
      },
      propList: ['*'],
    },
  },
};
```

### PC Browser Adaptation

Vant is a mobile-first component library. Use [@vant/touch-emulator](https://github.com/vant-ui/vant/tree/main/packages/vant-touch-emulator) for PC browsers:

```bash
# Install
npm i @vant/touch-emulator -S
```

```js
// Import this module, then Vant works in PC browser
import '@vant/touch-emulator';
```

## Built-in Styles

Vant provides common utility classes:

### Text Ellipsis

```html
<!-- Single line ellipsis -->
<div class="van-ellipsis">
  This is a paragraph that displays up to one line of text.
</div>

<!-- Multi-line ellipsis -->
<div class="van-multi-ellipsis--l2">
  This is a paragraph that displays up to two lines of text.
</div>

<div class="van-multi-ellipsis--l3">
  This is a paragraph that displays up to three lines of text.
</div>
```

### Hairline (1px Border)

```html
<div class="van-hairline--top"></div>
<div class="van-hairline--bottom"></div>
<div class="van-hairline--left"></div>
<div class="van-hairline--right"></div>
<div class="van-hairline--top-bottom"></div>
<div class="van-hairline--surround"></div>
```

### Safe Area

```html
<div class="van-safe-area-top"></div>
<div class="van-safe-area-bottom"></div>
```

### Animations

```html
<!-- fade in -->
<transition name="van-fade">
  <div v-show="visible">Fade</div>
</transition>

<!-- slide up -->
<transition name="van-slide-up">
  <div v-show="visible">Slide Up</div>
</transition>

<!-- slide down -->
<transition name="van-slide-down">
  <div v-show="visible">Slide Down</div>
</transition>

<!-- slide left -->
<transition name="van-slide-left">
  <div v-show="visible">Slide Left</div>
</transition>

<!-- slide right -->
<transition name="van-slide-right">
  <div v-show="visible">Slide Right</div>
</transition>
```

### Haptics Feedback

```html
<div class="van-haptics-feedback"></div>
```

### Clearfix

```html
<div class="van-clearfix"></div>
```

## Performance Optimization

### Tree Shaking

Vant supports Tree Shaking by default. Import only the components you need:

```js
import { Button, Cell } from 'vant';
```

### On-Demand Import

Use `unplugin-vue-components` for automatic on-demand import:

```js
import { VantResolver } from '@vant/auto-import-resolver';

Components({
  resolvers: [VantResolver()],
});
```

### Lazy Loading Components

For Nuxt 3, use `Lazy` prefix:

```html
<LazyVanButton type="default">lazy button</LazyVanButton>
```

### Image Lazy Loading

Use the Lazyload directive:

```js
import { Lazyload } from 'vant';

app.use(Lazyload, {
  lazyComponent: true,
});
```

```html
<van-image lazy-load src="https://example.com/image.jpg" />
```

## Best Practices

1. **Use on-demand import**: Reduce bundle size by importing only needed components.

2. **Choose the right unit**: Use viewport units for responsive design, rem for flexible scaling.

3. **Lazy load images**: Improve performance with lazy loading for images.

4. **Use built-in styles**: Leverage Vant's utility classes for common patterns.

5. **Avoid full registration**: Only register all components when necessary.

6. **PC adaptation**: Use touch-emulator for desktop browsers.

## Input Parameters

When using this skill, provide the following information:
- **Registration method**: Global, local, or on-demand
- **Screen adaptation**: Viewport units, rem, or none
- **Target platform**: Mobile, PC, or both
- **Performance needs**: Bundle size optimization requirements

## Output Format

This skill provides:
1. Component registration code examples
2. PostCSS configuration for unit conversion
3. PC browser adaptation setup
4. Built-in style usage examples
5. Performance optimization recommendations

## Usage Limitations

- PC adaptation requires additional touch-emulator package
- Viewport units may have compatibility issues in older browsers
- Full registration significantly increases bundle size
- Some PostCSS plugins require specific configuration for Vant
