---
name: "van-address-list"
description: "Address list component for displaying and managing multiple receiving addresses. Invoke when user needs to implement address selection or management functionality."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant AddressList Component

Display a list of receiving addresses with selection, editing, and management features.

## When to Invoke

Invoke this skill when:
- User needs to display a list of addresses
- User wants to implement address selection functionality
- User needs to manage multiple addresses (add, edit, delete)
- User wants to show disabled/unavailable addresses
- User asks about default address handling
- User needs address list with radio selection

## Features

- **Address Display**: Show multiple addresses in a list format
- **Address Selection**: Single or multiple address selection support
- **Default Address**: Visual indicator for default address
- **Disabled Addresses**: Support for showing unavailable addresses
- **Edit Actions**: Built-in edit button for each address
- **Add Button**: Quick access to add new address
- **Customizable**: Custom content via slots

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model | ID of chosen address, supports multiple selection (array type) | `number \| string \| number[] \| string[]` | - |
| list | Address list data | `Address[]` | `[]` |
| disabled-list | Disabled address list | `Address[]` | `[]` |
| disabled-text | Text description for disabled addresses | `string` | - |
| switchable | Whether to allow switching address | `boolean` | `true` |
| show-add-button | Whether to show add button | `boolean` | `true` |
| add-button-text | Text for add button | `string` | `Add new address` |
| default-tag-text | Text for default address tag | `string` | - |
| right-icon | Right icon name | `string` | `edit` |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| add | Emitted when add button is clicked | - |
| edit | Emitted when edit icon is clicked | `item: Address, index: number` |
| select | Emitted when an address is selected | `item: Address, index: number` |
| edit-disabled | Emitted when edit icon of disabled address is clicked | `item: Address, index: number` |
| select-disabled | Emitted when a disabled address is selected | `item: Address, index: number` |
| click-item | Emitted when an address item is clicked | `item: Address, index: number, { event }` |

### Address Data Structure

| Key | Description | Type |
|-----|-------------|------|
| id | Unique identifier | `number \| string` |
| name | Recipient name | `string` |
| tel | Phone number | `number \| string` |
| address | Full address | `string` |
| isDefault | Whether it's the default address | `boolean` |

### Slots

| Name | Description | SlotProps |
|------|-------------|-----------|
| default | Custom content after list | - |
| top | Custom content before list | - |
| item-bottom | Custom content after each list item | `item: Address` |
| tag | Custom tag for list item | `item: Address` |

### Types

```ts
import type { AddressListProps, AddressListAddress } from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-address-list
    v-model="chosenAddressId"
    :list="list"
    :disabled-list="disabledList"
    disabled-text="The following address is out of range"
    default-tag-text="Default"
    @add="onAdd"
    @edit="onEdit"
    @select="onSelect"
  />
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const chosenAddressId = ref('1');

const list = ref([
  {
    id: '1',
    name: 'John Snow',
    tel: '13000000000',
    address: 'Somewhere in Beijing',
    isDefault: true,
  },
  {
    id: '2',
    name: 'Ned Stark',
    tel: '13100000000',
    address: 'Somewhere in Shanghai',
    isDefault: false,
  },
]);

const disabledList = ref([
  {
    id: '3',
    name: 'Tywin Lannister',
    tel: '13200000000',
    address: 'Somewhere in Guangzhou',
  },
]);

const onAdd = () => {
  showToast('Add new address');
};

const onEdit = (item, index) => {
  showToast(`Edit address: ${index}`);
};

const onSelect = (item, index) => {
  showToast(`Selected: ${item.name}`);
};
</script>
```

### Multiple Selection

```vue
<template>
  <van-address-list
    v-model="selectedIds"
    :list="list"
    @select="onSelect"
  />
</template>

<script setup>
import { ref } from 'vue';

const selectedIds = ref(['1', '2']);

const list = ref([
  { id: '1', name: 'John', tel: '13000000000', address: 'Beijing' },
  { id: '2', name: 'Jane', tel: '13100000000', address: 'Shanghai' },
  { id: '3', name: 'Bob', tel: '13200000000', address: 'Guangzhou' },
]);

const onSelect = (item) => {
  console.log('Selected:', item);
};
</script>
```

### With Custom Content

```vue
<template>
  <van-address-list
    v-model="chosenAddressId"
    :list="list"
    default-tag-text="Default"
    @add="onAdd"
    @edit="onEdit"
  >
    <template #top>
      <van-notice-bar>Please select a delivery address</van-notice-bar>
    </template>
    <template #item-bottom="{ item }">
      <div class="address-time">
        Last used: {{ item.lastUsed }}
      </div>
    </template>
  </van-address-list>
</template>

<script setup>
import { ref } from 'vue';

const chosenAddressId = ref('1');

const list = ref([
  {
    id: '1',
    name: 'John Snow',
    tel: '13000000000',
    address: 'Beijing',
    lastUsed: '2024-01-15',
  },
]);

const onAdd = () => console.log('Add');
const onEdit = (item) => console.log('Edit:', item);
</script>
```

### Without Add Button

```vue
<template>
  <van-address-list
    v-model="chosenAddressId"
    :list="list"
    :show-add-button="false"
    @select="onSelect"
  />
</template>

<script setup>
import { ref } from 'vue';

const chosenAddressId = ref('1');
const list = ref([
  { id: '1', name: 'John', tel: '13000000000', address: 'Beijing' },
]);

const onSelect = (item) => {
  console.log('Selected:', item);
};
</script>
```

### With Custom Right Icon

```vue
<template>
  <van-address-list
    v-model="chosenAddressId"
    :list="list"
    right-icon="arrow"
    @click-item="onClickItem"
  />
</template>

<script setup>
import { ref } from 'vue';

const chosenAddressId = ref('1');
const list = ref([
  { id: '1', name: 'John', tel: '13000000000', address: 'Beijing' },
]);

const onClickItem = (item, index, { event }) => {
  console.log('Clicked:', item);
};
</script>
```

### Non-Switchable Mode

```vue
<template>
  <van-address-list
    v-model="chosenAddressId"
    :list="list"
    :switchable="false"
    @edit="onEdit"
  />
</template>

<script setup>
import { ref } from 'vue';

const chosenAddressId = ref('1');
const list = ref([
  { id: '1', name: 'John', tel: '13000000000', address: 'Beijing' },
]);

const onEdit = (item) => {
  console.log('Edit:', item);
};
</script>
```

## Best Practices

1. **Default Address**: Mark one address as default using `isDefault` property
2. **Disabled Addresses**: Use `disabled-list` for addresses that cannot be used
3. **User Feedback**: Provide clear feedback when address is selected or edited
4. **Empty State**: Handle empty list gracefully with appropriate UI
5. **Address Validation**: Validate address data before displaying
6. **Performance**: For large lists, consider pagination or virtual scrolling
