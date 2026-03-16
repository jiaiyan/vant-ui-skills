---
name: "van-floating-panel"
description: "Floating panel component for creating bottom draggable panels. Invoke when user needs to implement bottom sheets, expandable content panels, or draggable information displays."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant FloatingPanel Component

A panel that floats at the bottom of a page, which can be dragged up and down to browse content, commonly used for additional functionality or information.

## When to Invoke

Invoke this skill when:
- User needs to implement a bottom sheet panel
- User wants a draggable content panel
- User needs to show expandable information
- User asks about implementing map overlays
- User wants multi-height anchor points

## Features

- **Draggable**: Smooth drag up/down interactions
- **Custom Anchors**: Define multiple height anchor points
- **Magnetic Adsorption**: Auto-snap to nearest anchor
- **Height Control**: Control height via v-model
- **Content Drag**: Optional content area dragging
- **Safe Area**: Bottom safe area adaptation

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model:height | Current display height of the panel | `number \| string` | `0` |
| anchors | Custom anchor positions, unit `px` | `number[]` | `[100, window.innerHeight * 0.6]` |
| duration | Transition duration, unit second | `number \| string` | `0.3` |
| magnetic | Enable magnetic adsorption to anchors | `boolean` | `true` |
| content-draggable | Allow dragging content | `boolean` | `true` |
| draggable | Whether to allow dragging the panel | `boolean` | `true` |
| lock-scroll | Lock background scroll when not dragging | `boolean` | `false` |
| safe-area-inset-bottom | Enable bottom safe area adaptation | `boolean` | `true` |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| height-change | Emitted when panel height changes after dragging | `{ height: number }` |

### Slots

| Name | Description |
|------|-------------|
| default | Custom panel content |
| header | Custom panel header |

### Types

```ts
import type { FloatingPanelProps } from 'vant'
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-floating-panel>
    <van-cell-group>
      <van-cell
        v-for="i in 26"
        :key="i"
        :title="String.fromCharCode(i + 64)"
        size="large"
      />
    </van-cell-group>
  </van-floating-panel>
</template>
```

### Custom Anchors

```vue
<template>
  <van-floating-panel v-model:height="height" :anchors="anchors">
    <div style="text-align: center; padding: 15px">
      <p>Panel Height: {{ height.toFixed(0) }} px</p>
    </div>
  </van-floating-panel>
</template>

<script setup>
import { ref } from 'vue'

const anchors = [
  100,
  Math.round(0.4 * window.innerHeight),
  Math.round(0.7 * window.innerHeight)
]
const height = ref(anchors[0])
</script>
```

### Header Only Drag

```vue
<template>
  <van-floating-panel :content-draggable="false">
    <div style="text-align: center; padding: 15px">
      <p>Content cannot be dragged</p>
    </div>
  </van-floating-panel>
</template>
```

### Disable Magnetic Adsorption

```vue
<template>
  <van-floating-panel :anchors="[100, 200, 300]" :magnetic="false">
    <div style="text-align: center; padding: 15px">
      <p>Magnetic adsorption disabled</p>
      <p>Panel can stop at any position within boundaries</p>
    </div>
  </van-floating-panel>
</template>
```

### Disable Dragging

```vue
<template>
  <van-floating-panel :draggable="false">
    <div style="text-align: center; padding: 15px">
      <p>This panel cannot be dragged</p>
    </div>
  </van-floating-panel>
</template>
```

### Custom Header

```vue
<template>
  <van-floating-panel v-model:height="height" :anchors="anchors">
    <template #header>
      <div class="custom-header">
        <span>Drag to resize</span>
      </div>
    </template>
    
    <van-cell-group>
      <van-cell title="Item 1" />
      <van-cell title="Item 2" />
    </van-cell-group>
  </van-floating-panel>
</template>
```

## Common Issues

### 1. Panel Not Responding to Drag

Ensure `draggable` is not set to `false`:

```vue
<van-floating-panel :draggable="true">
  <!-- content -->
</van-floating-panel>
```

### 2. Content Scroll Conflict

Disable content dragging if you have scrollable content:

```vue
<van-floating-panel :content-draggable="false">
  <div style="overflow-y: auto; height: 100%;">
    <!-- scrollable content -->
  </div>
</van-floating-panel>
```

### 3. Initial Height Not Applied

Set `v-model:height` to one of the anchor values:

```vue
<script setup>
const anchors = [100, 200, 300]
const height = ref(anchors[0]) // Use first anchor
</script>
```

## Component Interactions

### With Map Overlay

```vue
<template>
  <div class="map-container">
    <map-component />
    
    <van-floating-panel 
      v-model:height="panelHeight" 
      :anchors="[80, 300, 500]"
    >
      <van-cell-group>
        <van-cell 
          v-for="place in nearbyPlaces" 
          :key="place.id"
          :title="place.name"
          :label="place.address"
        />
      </van-cell-group>
    </van-floating-panel>
  </div>
</template>
```

### With Tab Content

```vue
<template>
  <van-floating-panel v-model:height="height" :anchors="anchors">
    <van-tabs v-model:active="activeTab">
      <van-tab title="Details">
        <van-cell-group>
          <van-cell title="Name" value="Product Name" />
          <van-cell title="Price" value="$99.00" />
        </van-cell-group>
      </van-tab>
      <van-tab title="Reviews">
        <van-cell-group>
          <van-cell v-for="review in reviews" :key="review.id" :title="review.title" />
        </van-cell-group>
      </van-tab>
    </van-tabs>
  </van-floating-panel>
</template>
```

### With Action Buttons

```vue
<template>
  <van-floating-panel v-model:height="height" :anchors="[120, 400]">
    <div class="panel-content">
      <h3>Product Details</h3>
      <p>{{ product.description }}</p>
    </div>
    
    <template #header>
      <div class="panel-actions">
        <van-button type="primary" block>Add to Cart</van-button>
      </div>
    </template>
  </van-floating-panel>
</template>
```

## Best Practices

1. **Anchor points**: Define 2-3 meaningful anchor heights
2. **Content height**: Ensure content fits within maximum anchor
3. **Scroll handling**: Disable content-draggable for scrollable content
4. **Safe area**: Keep safe-area-inset-bottom enabled for iOS
5. **Performance**: Use lazy rendering for heavy content
6. **User feedback**: Show current height or state when relevant
