---
name: "van-popup"
description: "Popup component for displaying modal windows, information prompts, and overlays. Invoke when user needs to show popups, modals, or slide-out panels."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Popup Component

Used to display pop-up windows, information prompts, etc., and supports multiple pop-up layers to display.

## When to Invoke

Invoke this skill when:
- User needs to display a modal or popup
- User wants to create a bottom sheet or slide-out panel
- User needs to show overlay content
- User wants to create a dialog or confirmation box
- User asks about popup positioning or animations

## Features

- **Multiple Positions**: `center`, `top`, `bottom`, `left`, `right`
- **Round Corners**: Built-in rounded corner styles
- **Close Icon**: Customizable close icon with position options
- **Overlay Support**: Configurable overlay with custom styles
- **Animation**: Smooth transition animations
- **Teleport**: Mount to any DOM element
- **Safe Area**: Support for iOS safe area adaptation
- **Lock Scroll**: Prevent background scrolling

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model:show | Whether to show popup | `boolean` | `false` |
| overlay | Whether to show overlay | `boolean` | `true` |
| position | Popup position: `center` `top` `bottom` `right` `left` | `string` | `center` |
| overlay-class | Custom overlay class | `string \| Array \| object` | - |
| overlay-style | Custom overlay style | `object` | - |
| overlay-props | Overlay props | `object` | - |
| duration | Transition duration (seconds) | `number \| string` | `0.3` |
| z-index | Set z-index to a fixed value | `number \| string` | `2000+` |
| round | Whether to show round corner | `boolean` | `false` |
| destroy-on-close | Whether to destroy content when closed | `boolean` | `false` |
| lock-scroll | Whether to lock background scroll | `boolean` | `true` |
| lazy-render | Whether to lazy render until appeared | `boolean` | `true` |
| close-on-popstate | Whether to close when popstate | `boolean` | `false` |
| close-on-click-overlay | Whether to close when overlay is clicked | `boolean` | `true` |
| closeable | Whether to show close icon | `boolean` | `false` |
| close-icon | Close icon name | `string` | `cross` |
| close-icon-position | Close icon position: `top-left` `top-right` `bottom-left` `bottom-right` | `string` | `top-right` |
| before-close | Callback function before close | `(action: string) => boolean \| Promise<boolean>` | - |
| icon-prefix | Icon className prefix | `string` | `van-icon` |
| transition | Transition name | `string` | - |
| transition-appear | Whether to apply transition on initial render | `boolean` | `false` |
| teleport | Target element where Popup will be mounted | `string \| Element` | - |
| safe-area-inset-top | Whether to enable top safe area adaptation | `boolean` | `false` |
| safe-area-inset-bottom | Whether to enable bottom safe area adaptation | `boolean` | `false` |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| click | Emitted when Popup is clicked | `event: MouseEvent` |
| click-overlay | Emitted when overlay is clicked | `event: MouseEvent` |
| click-close-icon | Emitted when close icon is clicked | `event: MouseEvent` |
| open | Emitted immediately when Popup is opened | - |
| close | Emitted immediately when Popup is closed | - |
| opened | Emitted when Popup is opened and animation ends | - |
| closed | Emitted when Popup is closed and animation ends | - |

### Slots

| Name | Description |
|------|-------------|
| default | Content of Popup |
| overlay-content | Content of Popup overlay |

### Types

```ts
import type {
  PopupProps,
  PopupPosition,
  PopupInstance,
  PopupCloseIconPosition,
} from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-cell title="Show Popup" is-link @click="show = true" />
  <van-popup v-model:show="show" :style="{ padding: '64px' }">
    Content
  </van-popup>
</template>

<script setup>
import { ref } from 'vue';

const show = ref(false);
</script>
```

### Position Variants

```vue
<template>
  <van-button @click="showTop = true">Top Popup</van-button>
  <van-button @click="showBottom = true">Bottom Popup</van-button>
  <van-button @click="showLeft = true">Left Popup</van-button>
  <van-button @click="showRight = true">Right Popup</van-button>

  <van-popup v-model:show="showTop" position="top" :style="{ height: '30%' }" />
  <van-popup v-model:show="showBottom" position="bottom" :style="{ height: '30%' }" />
  <van-popup v-model:show="showLeft" position="left" :style="{ width: '30%', height: '100%' }" />
  <van-popup v-model:show="showRight" position="right" :style="{ width: '30%', height: '100%' }" />
</template>

<script setup>
import { ref } from 'vue';

const showTop = ref(false);
const showBottom = ref(false);
const showLeft = ref(false);
const showRight = ref(false);
</script>
```

### Close Icon

```vue
<template>
  <van-popup
    v-model:show="show"
    closeable
    position="bottom"
    :style="{ height: '30%' }"
  />

  <van-popup
    v-model:show="showCustom"
    closeable
    close-icon="close"
    position="bottom"
    :style="{ height: '30%' }"
  />

  <van-popup
    v-model:show="showPosition"
    closeable
    close-icon-position="top-left"
    position="bottom"
    :style="{ height: '30%' }"
  />
</template>

<script setup>
import { ref } from 'vue';

const show = ref(false);
const showCustom = ref(false);
const showPosition = ref(false);
</script>
```

### Round Corner

```vue
<template>
  <van-popup
    v-model:show="showCenter"
    round
    :style="{ padding: '64px' }"
  />

  <van-popup
    v-model:show="showBottom"
    round
    position="bottom"
    :style="{ height: '30%' }"
  />
</template>

<script setup>
import { ref } from 'vue';

const showCenter = ref(false);
const showBottom = ref(false);
</script>
```

### Listen to Events

```vue
<template>
  <van-cell title="Listen Click Events" is-link @click="show = true" />
  <van-popup
    v-model:show="show"
    position="bottom"
    :style="{ height: '30%' }"
    closeable
    @click-overlay="onClickOverlay"
    @click-close-icon="onClickCloseIcon"
    @open="onOpen"
    @opened="onOpened"
    @close="onClose"
    @closed="onClosed"
  />
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const show = ref(false);

const onClickOverlay = () => showToast('click-overlay');
const onClickCloseIcon = () => showToast('click-close-icon');
const onOpen = () => showToast('open');
const onOpened = () => showToast('opened');
const onClose = () => showToast('close');
const onClosed = () => showToast('closed');
</script>
```

### Before Close

```vue
<template>
  <van-popup
    v-model:show="show"
    position="bottom"
    :style="{ height: '30%' }"
    :before-close="beforeClose"
  >
    <div style="padding: 20px;">
      <p>Are you sure to close?</p>
      <van-button type="primary" @click="confirmClose">Confirm</van-button>
    </div>
  </van-popup>
</template>

<script setup>
import { ref } from 'vue';

const show = ref(false);
let resolveClose = null;

const beforeClose = () => {
  return new Promise((resolve) => {
    resolveClose = resolve;
  });
};

const confirmClose = () => {
  if (resolveClose) {
    resolveClose(true);
    resolveClose = null;
  }
};
</script>
```

### Teleport

```vue
<template>
  <van-popup v-model:show="show" teleport="body" />
  <van-popup v-model:show="showApp" teleport="#app" />
</template>

<script setup>
import { ref } from 'vue';

const show = ref(false);
const showApp = ref(false);
</script>
```

### Bottom Sheet with Content

```vue
<template>
  <van-cell title="Show Bottom Sheet" is-link @click="show = true" />
  <van-popup
    v-model:show="show"
    position="bottom"
    round
    :style="{ height: '50%' }"
  >
    <div class="sheet-content">
      <h3>Select Option</h3>
      <van-cell-group>
        <van-cell title="Option 1" is-link @click="selectOption(1)" />
        <van-cell title="Option 2" is-link @click="selectOption(2)" />
        <van-cell title="Option 3" is-link @click="selectOption(3)" />
      </van-cell-group>
    </div>
  </van-popup>
</template>

<script setup>
import { ref } from 'vue';

const show = ref(false);

const selectOption = (option) => {
  console.log('Selected:', option);
  show.value = false;
};
</script>

<style scoped>
.sheet-content {
  padding: 16px;
}

.sheet-content h3 {
  margin-bottom: 16px;
  text-align: center;
}
</style>
```

## Best Practices

1. **Use appropriate position**: Choose position based on content type (bottom for actions, center for alerts)
2. **Add round corners**: Use `round` prop for better visual appearance on mobile
3. **Handle close events**: Implement proper close handling for user actions
4. **Use teleport**: Mount popup to body for proper z-index stacking
5. **Safe area**: Enable safe area for bottom popups on iOS devices
6. **Lazy render**: Keep `lazy-render` enabled for performance
