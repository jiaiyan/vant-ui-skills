---
name: "van-contact-card"
description: "Contact card component for displaying contact information in card format. Invoke when user needs to implement contact selection or display functionality."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant ContactCard Component

Display contact information in the form of cards, supporting add and edit modes.

## When to Invoke

Invoke this skill when:
- User needs to display contact information
- User wants to implement contact selection
- User needs to show add contact card
- User wants to display edit contact card
- User asks about contact information display
- User needs non-editable contact display

## Features

- **Add Mode**: Display add contact card with icon
- **Edit Mode**: Display existing contact information
- **Non-Editable**: Support for read-only display
- **Custom Text**: Customizable add button text
- **Click Events**: Handle card click interactions
- **Simple Integration**: Easy to integrate with contact list

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| type | Card type, can be `add` or `edit` | `string` | `add` |
| name | Contact name (for edit mode) | `string` | - |
| tel | Contact phone number (for edit mode) | `string` | - |
| add-text | Text for add card | `string` | `Add contact info` |
| editable | Whether to allow editing | `boolean` | `true` |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| click | Emitted when card is clicked | `event: MouseEvent` |

### Types

```ts
import type { ContactCardType, ContactCardProps } from 'vant';
```

## Usage Examples

### Add Contact Card

```vue
<template>
  <van-contact-card type="add" @click="onAdd" />
</template>

<script setup>
import { showToast } from 'vant';

const onAdd = () => {
  showToast('Add contact');
};
</script>
```

### Edit Contact Card

```vue
<template>
  <van-contact-card
    type="edit"
    :tel="tel"
    :name="name"
    @click="onEdit"
  />
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const tel = ref('13000000000');
const name = ref('John Snow');

const onEdit = () => {
  showToast('Edit contact');
};
</script>
```

### Non-Editable Contact Card

```vue
<template>
  <van-contact-card
    type="edit"
    name="John Snow"
    tel="13000000000"
    :editable="false"
  />
</template>
```

### Custom Add Text

```vue
<template>
  <van-contact-card
    type="add"
    add-text="Add new recipient"
    @click="onAdd"
  />
</template>

<script setup>
import { showToast } from 'vant';

const onAdd = () => {
  showToast('Add new recipient');
};
</script>
```

### With Contact Selection Flow

```vue
<template>
  <div>
    <van-contact-card
      :type="hasContact ? 'edit' : 'add'"
      :name="contact.name"
      :tel="contact.tel"
      @click="showList = true"
    />
    
    <van-popup v-model:show="showList" position="bottom" round>
      <van-contact-list
        v-model="selectedId"
        :list="contactList"
        @select="onSelect"
      />
    </van-popup>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const showList = ref(false);
const selectedId = ref('');
const contactList = ref([
  { id: '1', name: 'John Snow', tel: '13000000000' },
  { id: '2', name: 'Ned Stark', tel: '13100000000' },
]);

const contact = computed(() => {
  return contactList.value.find(item => item.id === selectedId.value) || {};
});

const hasContact = computed(() => {
  return !!selectedId.value;
});

const onSelect = (contact) => {
  showList.value = false;
};
</script>
```

### In Order Form

```vue
<template>
  <div class="order-form">
    <van-contact-card
      type="edit"
      :name="order.contactName"
      :tel="order.contactTel"
      @click="editContact"
    />
    
    <van-cell-group inset>
      <van-cell title="Delivery Address" :value="order.address" />
      <van-cell title="Delivery Time" :value="order.deliveryTime" />
    </van-cell-group>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const order = ref({
  contactName: 'John Snow',
  contactTel: '13000000000',
  address: 'Beijing, China',
  deliveryTime: 'ASAP',
});

const editContact = () => {
  showToast('Edit contact');
};
</script>
```

### Multiple Contact Cards

```vue
<template>
  <div>
    <van-cell-group inset>
      <van-cell title="Sender">
        <template #default>
          <van-contact-card
            type="edit"
            :name="sender.name"
            :tel="sender.tel"
            :editable="false"
          />
        </template>
      </van-cell>
      
      <van-cell title="Receiver">
        <template #default>
          <van-contact-card
            type="edit"
            :name="receiver.name"
            :tel="receiver.tel"
            @click="editReceiver"
          />
        </template>
      </van-cell>
    </van-cell-group>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const sender = ref({
  name: 'Sender Name',
  tel: '13000000000',
});

const receiver = ref({
  name: 'Receiver Name',
  tel: '13100000000',
});

const editReceiver = () => {
  showToast('Edit receiver');
};
</script>
```

## Best Practices

1. **Mode Selection**: Use `type="add"` for new contacts, `type="edit"` for existing
2. **Editable Control**: Set `editable="false"` for display-only scenarios
3. **Integration**: Combine with ContactList and ContactEdit for complete contact management
4. **User Feedback**: Provide clear feedback when card is clicked
5. **Data Validation**: Validate contact information before display
6. **Responsive Design**: Consider card width on different screen sizes
