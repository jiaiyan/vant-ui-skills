---
name: "van-card"
description: "Card component for displaying product information including images, prices, and descriptions. Invoke when user needs to implement product display or shopping cart items."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Card Component

Used to display product pictures, prices, and other information in a card format.

## When to Invoke

Invoke this skill when:
- User needs to display product information
- User wants to implement shopping cart items
- User needs to show product cards with images
- User wants to display price and discount information
- User asks about product card layouts
- User needs customizable card content

## Features

- **Product Display**: Show product image, title, description, and price
- **Price Formatting**: Built-in price display with currency symbol
- **Discount Tags**: Support for product tags and discount information
- **Origin Price**: Display original price with strikethrough
- **Lazy Loading**: Support for image lazy loading
- **Custom Slots**: Flexible content customization via slots
- **Click Events**: Handle click events on card and thumbnail

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| thumb | Left thumbnail image URL | `string` | - |
| title | Product title | `string` | - |
| desc | Product description | `string` | - |
| tag | Product tag | `string` | - |
| num | Product quantity | `number \| string` | - |
| price | Product price | `number \| string` | - |
| origin-price | Original price (for discount display) | `number \| string` | - |
| centered | Whether content is vertically centered | `boolean` | `false` |
| currency | Currency symbol | `string` | `¥` |
| thumb-link | Link URL for thumbnail click | `string` | - |
| lazy-load | Whether to enable lazy loading for thumbnail | `boolean` | `false` |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| click | Emitted when card is clicked | `event: MouseEvent` |
| click-thumb | Emitted when thumbnail is clicked | `event: MouseEvent` |

### Slots

| Name | Description |
|------|-------------|
| title | Custom title content |
| desc | Custom description content |
| num | Custom quantity display |
| price | Custom price display |
| origin-price | Custom original price display |
| price-top | Custom content above price |
| bottom | Custom content below price |
| thumb | Custom thumbnail content |
| tag | Custom tag on thumbnail |
| tags | Custom tags area |
| footer | Custom footer content |

### Types

```ts
import type { CardProps } from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-card
    num="2"
    price="2.00"
    title="Product Title"
    desc="Product description"
    thumb="https://fastly.jsdelivr.net/npm/@vant/assets/ipad.jpeg"
  />
</template>
```

### With Discount Info

```vue
<template>
  <van-card
    num="2"
    tag="Discount"
    price="2.00"
    origin-price="10.00"
    title="Product Title"
    desc="Product description"
    thumb="https://fastly.jsdelivr.net/npm/@vant/assets/ipad.jpeg"
  />
</template>
```

### With Custom Tags

```vue
<template>
  <van-card
    num="2"
    price="2.00"
    title="Product Title"
    desc="Product description"
    thumb="https://fastly.jsdelivr.net/npm/@vant/assets/ipad.jpeg"
  >
    <template #tags>
      <van-tag plain type="primary">Tag 1</van-tag>
      <van-tag plain type="primary">Tag 2</van-tag>
    </template>
  </van-card>
</template>
```

### With Footer Buttons

```vue
<template>
  <van-card
    num="2"
    price="2.00"
    title="Product Title"
    desc="Product description"
    thumb="https://fastly.jsdelivr.net/npm/@vant/assets/ipad.jpeg"
  >
    <template #footer>
      <van-button size="mini">Button</van-button>
      <van-button size="mini">Button</van-button>
    </template>
  </van-card>
</template>
```

### Shopping Cart Item

```vue
<template>
  <van-card
    :num="item.num"
    :price="item.price"
    :title="item.title"
    :desc="item.desc"
    :thumb="item.thumb"
  >
    <template #footer>
      <van-stepper v-model="item.num" min="1" max="99" />
    </template>
  </van-card>
</template>

<script setup>
import { ref } from 'vue';

const item = ref({
  id: 1,
  title: 'iPad Pro',
  desc: '12.9-inch, 256GB, Wi-Fi',
  price: '9999.00',
  num: 1,
  thumb: 'https://fastly.jsdelivr.net/npm/@vant/assets/ipad.jpeg',
});
</script>
```

### With Click Events

```vue
<template>
  <van-card
    num="2"
    price="2.00"
    title="Product Title"
    desc="Product description"
    thumb="https://fastly.jsdelivr.net/npm/@vant/assets/ipad.jpeg"
    thumb-link="/product/1"
    @click="onClick"
    @click-thumb="onClickThumb"
  />
</template>

<script setup>
import { showToast } from 'vant';

const onClick = () => {
  showToast('Card clicked');
};

const onClickThumb = () => {
  showToast('Thumbnail clicked');
};
</script>
```

### Centered Layout

```vue
<template>
  <van-card
    centered
    price="2.00"
    title="Product Title"
    desc="Product description"
    thumb="https://fastly.jsdelivr.net/npm/@vant/assets/ipad.jpeg"
  />
</template>
```

### With Lazy Loading

```vue
<template>
  <van-card
    lazy-load
    price="2.00"
    title="Product Title"
    desc="Product description"
    thumb="https://fastly.jsdelivr.net/npm/@vant/assets/ipad.jpeg"
  />
</template>

<script setup>
import { Lazyload } from 'vant';

// Register Lazyload directive
// app.use(Lazyload);
</script>
```

### Custom Currency

```vue
<template>
  <van-card
    num="2"
    price="2.00"
    currency="$"
    title="Product Title"
    desc="Product description"
    thumb="https://fastly.jsdelivr.net/npm/@vant/assets/ipad.jpeg"
  />
</template>
```

### Fully Customized

```vue
<template>
  <van-card
    :thumb="product.thumb"
  >
    <template #title>
      <div class="custom-title">{{ product.title }}</div>
    </template>
    <template #desc>
      <div class="custom-desc">{{ product.desc }}</div>
    </template>
    <template #price>
      <div class="custom-price">
        <span class="current">¥{{ product.price }}</span>
        <span class="original">¥{{ product.originalPrice }}</span>
      </div>
    </template>
    <template #num>
      <van-stepper v-model="product.num" />
    </template>
    <template #footer>
      <van-button size="small" type="danger" @click="remove">Remove</van-button>
    </template>
  </van-card>
</template>

<script setup>
import { ref } from 'vue';

const product = ref({
  title: 'Custom Product',
  desc: 'Custom description',
  price: '99.00',
  originalPrice: '199.00',
  num: 1,
  thumb: 'https://fastly.jsdelivr.net/npm/@vant/assets/ipad.jpeg',
});

const remove = () => {
  console.log('Remove product');
};
</script>
```

## Best Practices

1. **Image Optimization**: Use optimized images for thumbnails
2. **Lazy Loading**: Enable lazy loading for better performance with many cards
3. **Price Formatting**: Use consistent decimal places for prices
4. **Responsive Design**: Consider card width on different screen sizes
5. **Accessibility**: Add meaningful alt text for product images
6. **Click Feedback**: Provide visual feedback when card is clicked
7. **Quantity Control**: Use Stepper component for quantity adjustment in cart items
