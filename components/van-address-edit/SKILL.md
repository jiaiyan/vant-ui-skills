---
name: "van-address-edit"
description: "Address editing component for creating, updating, and deleting receiving addresses. Invoke when user needs to implement address management functionality."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant AddressEdit Component

Used to create, update, and delete receiving addresses.

## When to Invoke

Invoke this skill when:
- User needs to implement address creation functionality
- User wants to edit existing address information
- User needs to delete address functionality
- User wants to set default address
- User asks about address form validation
- User needs address search or autocomplete features

## Features

- **Address Management**: Create, update, and delete addresses
- **Area Selection**: Three-level linkage for province/city/district selection
- **Address Search**: Support for address search and autocomplete
- **Default Address**: Option to set address as default
- **Form Validation**: Built-in validation for phone numbers and other fields
- **Custom Validation**: Support for custom validation functions
- **Loading States**: Loading status for save and delete operations
- **Flexible Layout**: Configurable visibility for area and detail fields

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| area-list | Area list data for province/city/district selection | `object` | - |
| area-columns-placeholder | Placeholder text for area columns | `string[]` | `[]` |
| area-placeholder | Placeholder for area input field | `string` | `Area` |
| address-info | Initial address information | `AddressEditInfo` | `{}` |
| search-result | Address search results | `AddressEditSearchItem[]` | `[]` |
| show-delete | Whether to show delete button | `boolean` | `false` |
| show-set-default | Whether to show default address switch | `boolean` | `false` |
| show-search-result | Whether to show address search results | `boolean` | `false` |
| show-area | Whether to show area selection cell | `boolean` | `true` |
| show-detail | Whether to show detail address field | `boolean` | `true` |
| disable-area | Whether to disable area selection | `boolean` | `false` |
| save-button-text | Text for save button | `string` | `Save` |
| delete-button-text | Text for delete button | `string` | `Delete` |
| detail-rows | Number of rows for detail input | `number \| string` | `1` |
| detail-maxlength | Maximum length for detail address | `number \| string` | `200` |
| is-saving | Whether to show loading on save button | `boolean` | `false` |
| is-deleting | Whether to show loading on delete button | `boolean` | `false` |
| tel-validator | Custom phone number validator | `(val: string) => boolean` | - |
| tel-maxlength | Maximum length for phone number | `number \| string` | - |
| validator | Custom field validator | `(key: string, val: string) => string` | - |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| save | Emitted when save button is clicked | `info: AddressEditInfo` |
| focus | Emitted when a field is focused | `key: string` |
| change | Emitted when name or tel field changes | `{key: string, value: string}` |
| delete | Emitted when delete is confirmed | `info: AddressEditInfo` |
| select-search | Emitted when a search result is selected | `value: string` |
| click-area | Emitted when area field is clicked | - |
| change-area | Emitted when area selection changes | `selectedOptions: PickerOption[]` |
| change-detail | Emitted when address detail changes | `value: string` |
| change-default | Emitted when default address switch changes | `checked: boolean` |

### Slots

| Name | Description |
|------|-------------|
| default | Custom content below address detail |

### Methods

Use [ref](https://vuejs.org/guide/essentials/template-refs.html) to get AddressEdit instance and call instance methods.

| Name | Description | Parameter | Return |
|------|-------------|-----------|--------|
| setAddressDetail | Set address detail text | `addressDetail: string` | - |
| setAreaCode | Set area code | `code: string` | - |

### Types

```ts
import type {
  AddressEditInfo,
  AddressEditProps,
  AddressEditInstance,
  AddressEditSearchItem,
} from 'vant';
```

### AddressEditInfo Data Structure

| Key | Description | Type |
|-----|-------------|------|
| name | Recipient name | `string` |
| tel | Phone number | `string` |
| province | Province name | `string` |
| city | City name | `string` |
| county | County/District name | `string` |
| addressDetail | Detailed address | `string` |
| areaCode | Area code | `string` |
| isDefault | Whether it's the default address | `boolean` |

### AddressEditSearchItem Data Structure

| Key | Description | Type |
|-----|-------------|------|
| name | Place name | `string` |
| address | Place address | `string` |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-address-edit
    :area-list="areaList"
    show-delete
    show-set-default
    show-search-result
    :search-result="searchResult"
    :area-columns-placeholder="['Choose', 'Choose', 'Choose']"
    @save="onSave"
    @delete="onDelete"
    @change-detail="onChangeDetail"
  />
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';
import { areaList } from '@vant/area-data';

const searchResult = ref([]);

const onSave = (info) => {
  showToast('Save');
  console.log('Address saved:', info);
};

const onDelete = (info) => {
  showToast('Delete');
  console.log('Address deleted:', info);
};

const onChangeDetail = (val) => {
  if (val) {
    searchResult.value = [
      { name: 'Name1', address: 'Address1' },
      { name: 'Name2', address: 'Address2' },
    ];
  } else {
    searchResult.value = [];
  }
};
</script>
```

### Edit Existing Address

```vue
<template>
  <van-address-edit
    :area-list="areaList"
    :address-info="addressInfo"
    show-delete
    show-set-default
    @save="onSave"
    @delete="onDelete"
  />
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';
import { areaList } from '@vant/area-data';

const addressInfo = ref({
  name: 'John Snow',
  tel: '13000000000',
  province: 'Zhejiang Province',
  city: 'Hangzhou',
  county: 'West Lake District',
  addressDetail: '123 Main Street',
  areaCode: '330106',
  isDefault: true,
});

const onSave = (info) => {
  showToast('Address updated');
};

const onDelete = (info) => {
  showToast('Address deleted');
};
</script>
```

### With Loading States

```vue
<template>
  <van-address-edit
    :area-list="areaList"
    :is-saving="saving"
    :is-deleting="deleting"
    show-delete
    @save="onSave"
    @delete="onDelete"
  />
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';
import { areaList } from '@vant/area-data';

const saving = ref(false);
const deleting = ref(false);

const onSave = async (info) => {
  saving.value = true;
  try {
    await saveAddress(info);
    showToast('Saved successfully');
  } finally {
    saving.value = false;
  }
};

const onDelete = async (info) => {
  deleting.value = true;
  try {
    await deleteAddress(info);
    showToast('Deleted successfully');
  } finally {
    deleting.value = false;
  }
};
</script>
```

### With Custom Validation

```vue
<template>
  <van-address-edit
    :area-list="areaList"
    :tel-validator="telValidator"
    :validator="customValidator"
    @save="onSave"
  />
</template>

<script setup>
import { areaList } from '@vant/area-data';

const telValidator = (tel) => {
  return /^1[3-9]\d{9}$/.test(tel);
};

const customValidator = (key, value) => {
  if (key === 'name' && !value.trim()) {
    return 'Name is required';
  }
  if (key === 'tel' && !/^1[3-9]\d{9}$/.test(value)) {
    return 'Invalid phone number';
  }
  return '';
};

const onSave = (info) => {
  console.log('Valid address:', info);
};
</script>
```

### Using Methods

```vue
<template>
  <van-address-edit
    ref="addressEditRef"
    :area-list="areaList"
    @save="onSave"
  />
  <van-button @click="setDetail">Set Detail</van-button>
  <van-button @click="setArea">Set Area</van-button>
</template>

<script setup>
import { ref } from 'vue';
import { areaList } from '@vant/area-data';

const addressEditRef = ref();

const setDetail = () => {
  addressEditRef.value?.setAddressDetail('123 Main Street');
};

const setArea = () => {
  addressEditRef.value?.setAreaCode('330106');
};

const onSave = (info) => {
  console.log('Address:', info);
};
</script>
```

### Without Area Selection

```vue
<template>
  <van-address-edit
    :area-list="areaList"
    :show-area="false"
    @save="onSave"
  />
</template>

<script setup>
import { areaList } from '@vant/area-data';

const onSave = (info) => {
  console.log('Address without area:', info);
};
</script>
```

## Best Practices

1. **Use Official Area Data**: Import `@vant/area-data` for China province/city/district data
2. **Validate Phone Numbers**: Use `tel-validator` for custom phone validation
3. **Handle Loading States**: Show loading indicators during async operations
4. **Provide Feedback**: Show toast messages after save/delete operations
5. **Pre-fill Data**: Use `address-info` when editing existing addresses
6. **Custom Validation**: Implement `validator` for comprehensive form validation
7. **Search Integration**: Use `search-result` and `show-search-result` for address autocomplete
