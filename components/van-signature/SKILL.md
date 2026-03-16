---
name: "van-signature"
description: "Signature component for capturing signatures on canvas. Invoke when user needs to implement signature capture, drawing pads, or canvas-based input."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Signature Component

Signature component for capturing signatures on canvas with customizable styling.

## When to Invoke

Invoke this skill when:
- User needs to implement signature capture functionality
- User wants to create a drawing or sketch pad
- User needs to capture handwritten signatures
- User wants to customize pen color or line width
- User asks about canvas-based signature export

## Features

- **Canvas-Based**: Built on HTML5 Canvas for smooth drawing
- **Custom Pen**: Configurable pen color and line width
- **Custom Background**: Set custom background color
- **Image Export**: Export signature as PNG or other formats
- **Clear & Confirm**: Built-in clear and confirm buttons
- **Touch Support**: Optimized for touch devices
- **Resize Support**: Automatic resize on container changes
- **Custom Tips**: Customizable placeholder text

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| type | Export image type | `string` | `png` |
| pen-color | Color of the brush stroke | `string` | `#000` |
| line-width | Width of the line | `number` | `3` |
| background-color | Background color | `string` | - |
| tips | Text that appears when Canvas is not supported | `string` | - |
| clear-button-text | Clear button text | `string` | `Clear` |
| confirm-button-text | Confirm button text | `string` | `Confirm` |

### Events

| Event | Description | Callback Parameters |
|-------|-------------|---------------------|
| start | Emitted when signing starts | - |
| end | Emitted when signing ends | - |
| signing | Emitted when signing | `event: TouchEvent` |
| submit | Emitted when clicking the confirm button | `data: { image: string; canvas: HTMLCanvasElement }` |
| clear | Emitted when clicking the cancel button | - |

### Slots

| Name | Description | SlotProps |
|------|-------------|-----------|
| tips | Custom tips | - |

### Methods

| Name | Description | Attribute | Return value |
|------|-------------|-----------|--------------|
| resize | Resize Signature when container element resized | - | - |
| clear | Clear the signature | - | - |
| submit | Trigger the `submit` event | - | - |

## Usage Examples

### Basic Usage

```vue
<template>
  <div>
    <van-signature @submit="onSubmit" @clear="onClear" />
    <van-image v-if="image" :src="image" />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const image = ref('')

const onSubmit = (data) => {
  image.value = data.image
}

const onClear = () => {
  showToast('Cleared')
}
</script>
```

### Custom Pen Color

```vue
<template>
  <van-signature 
    pen-color="#ff0000" 
    @submit="onSubmit" 
    @clear="onClear" 
  />
</template>

<script setup>
import { ref } from 'vue'

const image = ref('')

const onSubmit = (data) => {
  image.value = data.image
}

const onClear = () => {
  console.log('Cleared')
}
</script>
```

### Custom Line Width

```vue
<template>
  <van-signature 
    :line-width="6" 
    @submit="onSubmit" 
    @clear="onClear" 
  />
</template>

<script setup>
import { ref } from 'vue'

const image = ref('')

const onSubmit = (data) => {
  image.value = data.image
}

const onClear = () => {
  console.log('Cleared')
}
</script>
```

### Custom Background Color

```vue
<template>
  <van-signature 
    background-color="#eee" 
    @submit="onSubmit" 
    @clear="onClear" 
  />
</template>

<script setup>
import { ref } from 'vue'

const image = ref('')

const onSubmit = (data) => {
  image.value = data.image
}

const onClear = () => {
  console.log('Cleared')
}
</script>
```

### Using Methods

```vue
<template>
  <div>
    <van-signature 
      ref="signatureRef"
      @submit="onSubmit" 
      @clear="onClear" 
    />
    <div style="margin-top: 16px;">
      <van-button @click="clearSignature">Clear</van-button>
      <van-button type="primary" @click="submitSignature">Submit</van-button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const signatureRef = ref()
const image = ref('')

const onSubmit = (data) => {
  image.value = data.image
  showToast('Signature submitted')
}

const onClear = () => {
  showToast('Cleared')
}

const clearSignature = () => {
  signatureRef.value?.clear()
}

const submitSignature = () => {
  signatureRef.value?.submit()
}
</script>
```

### Signature Pad with Preview

```vue
<template>
  <div class="signature-page">
    <div class="signature-header">
      <h3>Please sign below</h3>
    </div>
    
    <van-signature 
      ref="signatureRef"
      pen-color="#000"
      :line-width="2"
      background-color="#fff"
      @submit="onSubmit"
      @clear="onClear"
    />
    
    <div v-if="signatureImage" class="signature-preview">
      <h4>Signature Preview:</h4>
      <van-image :src="signatureImage" fit="contain" />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const signatureRef = ref()
const signatureImage = ref('')

const onSubmit = (data) => {
  signatureImage.value = data.image
  showToast('Signature captured successfully')
}

const onClear = () => {
  signatureImage.value = ''
}
</script>

<style scoped>
.signature-page {
  padding: 16px;
}

.signature-header {
  margin-bottom: 16px;
}

.signature-header h3 {
  margin: 0;
  font-size: 16px;
  color: #323233;
}

.signature-preview {
  margin-top: 24px;
  padding: 16px;
  background: #f7f8fa;
  border-radius: 8px;
}

.signature-preview h4 {
  margin: 0 0 12px 0;
  font-size: 14px;
  color: #969799;
}
</style>
```

### Agreement Signature

```vue
<template>
  <div class="agreement-signature">
    <div class="agreement-content">
      <h3>User Agreement</h3>
      <p>Please read and sign the agreement below...</p>
      <div class="agreement-text">
        Lorem ipsum dolor sit amet, consectetur adipiscing elit...
      </div>
    </div>
    
    <div class="signature-section">
      <van-signature 
        ref="signatureRef"
        background-color="#fafafa"
        @submit="onSubmit"
        @clear="onClear"
      />
    </div>
    
    <div class="actions">
      <van-checkbox v-model="agreed">
        I agree to the terms and conditions
      </van-checkbox>
      <van-button 
        type="primary" 
        block 
        :disabled="!agreed || !hasSignature"
        @click="submitAgreement"
      >
        Submit Agreement
      </van-button>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import { showToast } from 'vant'

const signatureRef = ref()
const agreed = ref(false)
const signatureImage = ref('')

const hasSignature = computed(() => !!signatureImage.value)

const onSubmit = (data) => {
  signatureImage.value = data.image
}

const onClear = () => {
  signatureImage.value = ''
}

const submitAgreement = () => {
  showToast('Agreement submitted successfully')
}
</script>

<style scoped>
.agreement-signature {
  padding: 16px;
}

.agreement-content {
  margin-bottom: 24px;
}

.agreement-content h3 {
  margin: 0 0 12px 0;
  font-size: 18px;
  color: #323233;
}

.agreement-text {
  padding: 12px;
  background: #f7f8fa;
  border-radius: 4px;
  font-size: 14px;
  line-height: 1.6;
  max-height: 200px;
  overflow-y: auto;
}

.signature-section {
  margin-bottom: 16px;
}

.actions {
  display: flex;
  flex-direction: column;
  gap: 12px;
}
</style>
```

## Best Practices

1. **Clear Instructions**: Provide clear instructions for users
2. **Adequate Space**: Ensure sufficient canvas height for signatures
3. **Background Contrast**: Use contrasting background for visibility
4. **Pen Width**: Use appropriate line width for signature clarity
5. **Preview**: Show signature preview before final submission
6. **Validation**: Validate that signature is not empty before submission
7. **Export Format**: Choose appropriate export format (PNG recommended)
8. **Responsive**: Handle container resize with the resize method
