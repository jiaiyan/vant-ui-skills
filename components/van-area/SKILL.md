---
name: "van-area"
description: "Area selection component with three-level linkage for provinces, cities, and districts. Invoke when user needs to implement location selection functionality."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Area Component

A three-level linkage selection component for provinces, cities, and districts, typically used with the Popup component.

## When to Invoke

Invoke this skill when:
- User needs to select a province/city/district
- User wants to implement address location selection
- User needs area picker with three-level linkage
- User asks about China area data
- User wants to customize area columns
- User needs area selection with popup

## Features

- **Three-Level Linkage**: Province, city, and district selection
- **Flexible Columns**: Configurable number of columns (1-3 levels)
- **Model Binding**: Two-way binding with area code
- **Custom Data**: Support for custom area data
- **Official Data**: Integration with @vant/area-data package
- **Placeholder Support**: Customizable column placeholders
- **Popup Integration**: Works seamlessly with Popup component

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model | Code of selected area | `string` | - |
| title | Toolbar title | `string` | - |
| confirm-button-text | Text for confirm button | `string` | `Confirm` |
| cancel-button-text | Text for cancel button | `string` | `Cancel` |
| area-list | Area list data object | `object` | - |
| columns-placeholder | Placeholder text for columns | `string[]` | `[]` |
| loading | Whether to show loading state | `boolean` | `false` |
| readonly | Whether to be readonly | `boolean` | `false` |
| option-height | Option height (supports px, vw, vh, rem) | `number \| string` | `44` |
| columns-num | Number of picker columns (1-3) | `number \| string` | `3` |
| visible-option-num | Count of visible options | `number \| string` | `6` |
| swipe-duration | Duration of momentum animation (ms) | `number \| string` | `1000` |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| confirm | Emitted when confirm button is clicked | `{ selectedValues, selectedOptions, selectedIndexes }` |
| cancel | Emitted when cancel button is clicked | `{ selectedValues, selectedOptions, selectedIndexes }` |
| change | Emitted when current option changes | `{ selectedValues, selectedOptions, selectedIndexes, columnIndex }` |

### Slots

| Name | Description | SlotProps |
|------|-------------|-----------|
| toolbar | Custom toolbar content | - |
| title | Custom title | - |
| confirm | Custom confirm button text | - |
| cancel | Custom cancel button text | - |
| columns-top | Custom content above columns | - |
| columns-bottom | Custom content below columns | - |

### Methods

Use [ref](https://vuejs.org/guide/essentials/template-refs.html) to get Area instance and call instance methods.

| Name | Description | Parameter | Return |
|------|-------------|-----------|--------|
| confirm | Stop scrolling and emit confirm event | - | - |
| getSelectedOptions | Get current selected options | - | `PickerOption[]` |

### Types

```ts
import type { AreaProps, AreaList, AreaInstance, AreaColumnOption } from 'vant';
```

### AreaList Data Structure

```ts
interface AreaList {
  province_list: Record<string, string>;
  city_list: Record<string, string>;
  county_list: Record<string, string>;
}
```

The key is a 6-digit code:
- First 2 digits: Province code
- Middle 2 digits: City code
- Last 2 digits: District code

## Usage Examples

### Basic Usage

```vue
<template>
  <van-popup v-model:show="show" position="bottom" round>
    <van-area title="Select Area" :area-list="areaList" @confirm="onConfirm" @cancel="show = false" />
  </van-popup>
</template>

<script setup>
import { ref } from 'vue';
import { areaList } from '@vant/area-data';

const show = ref(false);

const onConfirm = ({ selectedOptions }) => {
  const areaName = selectedOptions.map(item => item.text).join('/');
  console.log('Selected area:', areaName);
  show.value = false;
};
</script>
```

### With Model Binding

```vue
<template>
  <van-field
    v-model="areaText"
    is-link
    readonly
    label="Area"
    placeholder="Select area"
    @click="show = true"
  />
  <van-popup v-model:show="show" position="bottom" round>
    <van-area
      v-model="areaCode"
      title="Select Area"
      :area-list="areaList"
      @confirm="onConfirm"
      @cancel="show = false"
    />
  </van-popup>
</template>

<script setup>
import { ref, computed } from 'vue';
import { areaList } from '@vant/area-data';

const show = ref(false);
const areaCode = ref('330302');

const areaText = computed(() => {
  const codes = areaCode.value;
  return codes;
});

const onConfirm = ({ selectedOptions }) => {
  areaCode.value = selectedOptions[2]?.value || '';
  show.value = false;
};
</script>
```

### Two-Level Selection

```vue
<template>
  <van-popup v-model:show="show" position="bottom" round>
    <van-area
      title="Select City"
      :area-list="areaList"
      :columns-num="2"
      @confirm="onConfirm"
    />
  </van-popup>
</template>

<script setup>
import { ref } from 'vue';
import { areaList } from '@vant/area-data';

const show = ref(false);

const onConfirm = ({ selectedOptions }) => {
  console.log('City:', selectedOptions);
};
</script>
```

### With Placeholders

```vue
<template>
  <van-popup v-model:show="show" position="bottom" round>
    <van-area
      title="Select Area"
      :area-list="areaList"
      :columns-placeholder="['Province', 'City', 'District']"
      @confirm="onConfirm"
    />
  </van-popup>
</template>

<script setup>
import { ref } from 'vue';
import { areaList } from '@vant/area-data';

const show = ref(false);

const onConfirm = ({ selectedOptions }) => {
  console.log('Selected:', selectedOptions);
};
</script>
```

### With Loading State

```vue
<template>
  <van-popup v-model:show="show" position="bottom" round>
    <van-area
      title="Select Area"
      :area-list="areaList"
      :loading="loading"
      @confirm="onConfirm"
    />
  </van-popup>
</template>

<script setup>
import { ref } from 'vue';

const show = ref(false);
const loading = ref(true);
const areaList = ref({});

const loadAreaData = async () => {
  loading.value = true;
  const { areaList: data } = await import('@vant/area-data');
  areaList.value = data;
  loading.value = false;
};

loadAreaData();

const onConfirm = ({ selectedOptions }) => {
  console.log('Selected:', selectedOptions);
};
</script>
```

### Using Methods

```vue
<template>
  <van-popup v-model:show="show" position="bottom" round>
    <van-area
      ref="areaRef"
      title="Select Area"
      :area-list="areaList"
      @confirm="onConfirm"
    />
  </van-popup>
  <van-button @click="getSelection">Get Selection</van-button>
</template>

<script setup>
import { ref } from 'vue';
import { areaList } from '@vant/area-data';

const show = ref(false);
const areaRef = ref();

const getSelection = () => {
  const options = areaRef.value?.getSelectedOptions();
  console.log('Current selection:', options);
};

const onConfirm = ({ selectedOptions }) => {
  console.log('Confirmed:', selectedOptions);
};
</script>
```

### Custom Area Data

```vue
<template>
  <van-popup v-model:show="show" position="bottom" round>
    <van-area title="Select Area" :area-list="customAreaList" @confirm="onConfirm" />
  </van-popup>
</template>

<script setup>
import { ref } from 'vue';

const show = ref(false);

const customAreaList = {
  province_list: {
    '110000': 'Beijing',
    '330000': 'Zhejiang',
  },
  city_list: {
    '110100': 'Beijing City',
    '330100': 'Hangzhou',
    '330200': 'Ningbo',
  },
  county_list: {
    '110101': 'Dongcheng District',
    '110102': 'Xicheng District',
    '330102': 'Shangcheng District',
    '330103': 'Xiacheng District',
  },
};

const onConfirm = ({ selectedOptions }) => {
  console.log('Selected:', selectedOptions);
};
</script>
```

## Best Practices

1. **Use Official Data**: Import `@vant/area-data` for China province/city/district data
2. **Popup Integration**: Always use with Popup component for better UX
3. **Loading State**: Show loading indicator when fetching area data asynchronously
4. **Default Selection**: Set `v-model` for pre-selecting an area
5. **Column Configuration**: Use `columns-num` for different selection levels
6. **Placeholder Text**: Use `columns-placeholder` for better user guidance
7. **Error Handling**: Handle cases where area data might not be available
