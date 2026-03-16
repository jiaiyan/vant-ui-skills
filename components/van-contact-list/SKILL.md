---
name: "van-contact-list"
description: "Contact list component for displaying and managing contacts. Invoke when user needs to implement contact selection or management functionality."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant ContactList Component

Used to display a list of contacts with selection and editing capabilities.

## When to Invoke

Invoke this skill when:
- User needs to display a list of contacts
- User wants to implement contact selection functionality
- User needs to manage multiple contacts
- User wants to show default contact indicator
- User asks about contact list with radio selection
- User needs contact management with add/edit features

## Features

- **Contact Display**: Show multiple contacts in a list format
- **Contact Selection**: Single contact selection support
- **Default Contact**: Visual indicator for default contact
- **Edit Actions**: Built-in edit button for each contact
- **Add Button**: Quick access to add new contact
- **Customizable**: Custom content via slots

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model | ID of chosen contact | `number \| string` | - |
| list | Contact list data | `ContactListItem[]` | `[]` |
| add-text | Text for add button | `string` | `Add new contact` |
| default-tag-text | Text for default contact tag | `string` | - |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| add | Emitted when add button is clicked | - |
| edit | Emitted when edit button is clicked | `contact: ContactListItem, index: number` |
| select | Emitted when a contact is selected | `contact: ContactListItem, index: number` |

### ContactListItem Data Structure

| Key | Description | Type |
|-----|-------------|------|
| id | Unique identifier | `number \| string` |
| name | Contact name | `string` |
| tel | Phone number | `string` |
| isDefault | Whether it's the default contact | `boolean \| undefined` |

### Types

```ts
import type { ContactListItem, ContactListProps } from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-contact-list
    v-model="chosenContactId"
    :list="list"
    default-tag-text="default"
    @add="onAdd"
    @edit="onEdit"
    @select="onSelect"
  />
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const chosenContactId = ref('1');

const list = ref([
  {
    id: '1',
    name: 'John Snow',
    tel: '13000000000',
    isDefault: true,
  },
  {
    id: '2',
    name: 'Ned Stark',
    tel: '13100000000',
    isDefault: false,
  },
]);

const onAdd = () => {
  showToast('Add contact');
};

const onEdit = (contact) => {
  showToast(`Edit contact: ${contact.id}`);
};

const onSelect = (contact) => {
  showToast(`Selected: ${contact.name}`);
};
</script>
```

### With Custom Add Text

```vue
<template>
  <van-contact-list
    v-model="chosenContactId"
    :list="list"
    add-text="Add new recipient"
    @add="onAdd"
  />
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const chosenContactId = ref('');
const list = ref([]);

const onAdd = () => {
  showToast('Add new recipient');
};
</script>
```

### Contact Selection for Order

```vue
<template>
  <div>
    <van-contact-list
      v-model="selectedContactId"
      :list="contacts"
      default-tag-text="Default"
      @select="onSelect"
    />
    
    <van-submit-bar
      :price="totalPrice"
      button-text="Submit Order"
      @submit="onSubmit"
    >
      <template #default>
        <span>Contact: {{ selectedContact?.name }}</span>
      </template>
    </van-submit-bar>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import { showToast } from 'vant';

const selectedContactId = ref('1');
const totalPrice = ref(9900);

const contacts = ref([
  { id: '1', name: 'John Snow', tel: '13000000000', isDefault: true },
  { id: '2', name: 'Ned Stark', tel: '13100000000', isDefault: false },
]);

const selectedContact = computed(() => {
  return contacts.value.find(c => c.id === selectedContactId.value);
});

const onSelect = (contact) => {
  showToast(`Selected: ${contact.name}`);
};

const onSubmit = () => {
  showToast('Order submitted');
};
</script>
```

### With Contact Management

```vue
<template>
  <div>
    <van-contact-list
      v-if="!showEdit"
      v-model="selectedId"
      :list="contactList"
      default-tag-text="Default"
      @add="onAdd"
      @edit="onEdit"
      @select="onSelect"
    />
    
    <van-contact-edit
      v-else
      :is-edit="isEditMode"
      :contact-info="editingContact"
      show-set-default
      @save="onSave"
      @delete="onDelete"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const showEdit = ref(false);
const isEditMode = ref(false);
const selectedId = ref('1');

const contactList = ref([
  { id: '1', name: 'John Snow', tel: '13000000000', isDefault: true },
  { id: '2', name: 'Ned Stark', tel: '13100000000', isDefault: false },
]);

const editingContact = ref({
  name: '',
  tel: '',
  isDefault: false,
});

const onAdd = () => {
  isEditMode.value = false;
  editingContact.value = { name: '', tel: '', isDefault: false };
  showEdit.value = true;
};

const onEdit = (contact) => {
  isEditMode.value = true;
  selectedId.value = contact.id;
  editingContact.value = { ...contact };
  showEdit.value = true;
};

const onSelect = (contact) => {
  console.log('Selected:', contact);
};

const onSave = (info) => {
  if (isEditMode.value) {
    const index = contactList.value.findIndex(c => c.id === selectedId.value);
    if (index > -1) {
      contactList.value[index] = { ...info, id: selectedId.value };
    }
  } else {
    contactList.value.push({
      ...info,
      id: Date.now().toString(),
    });
  }
  showEdit.value = false;
  showToast('Saved');
};

const onDelete = () => {
  contactList.value = contactList.value.filter(c => c.id !== selectedId.value);
  showEdit.value = false;
  showToast('Deleted');
};
</script>
```

### In Popup

```vue
<template>
  <div>
    <van-field
      v-model="contactDisplay"
      is-link
      readonly
      label="Contact"
      placeholder="Select contact"
      @click="showPopup = true"
    />
    
    <van-popup
      v-model:show="showPopup"
      position="bottom"
      round
      style="height: 60%"
    >
      <van-contact-list
        v-model="selectedId"
        :list="contacts"
        @select="onSelect"
      />
    </van-popup>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const showPopup = ref(false);
const selectedId = ref('');

const contacts = ref([
  { id: '1', name: 'John Snow', tel: '13000000000' },
  { id: '2', name: 'Ned Stark', tel: '13100000000' },
]);

const contactDisplay = computed(() => {
  const contact = contacts.value.find(c => c.id === selectedId.value);
  return contact ? `${contact.name} (${contact.tel})` : '';
});

const onSelect = (contact) => {
  showPopup.value = false;
};
</script>
```

### Empty State Handling

```vue
<template>
  <div>
    <van-empty
      v-if="contactList.length === 0"
      description="No contacts"
    >
      <van-button type="primary" @click="onAdd">Add Contact</van-button>
    </van-empty>
    
    <van-contact-list
      v-else
      v-model="selectedId"
      :list="contactList"
      @add="onAdd"
      @edit="onEdit"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue';

const selectedId = ref('');
const contactList = ref([]);

const onAdd = () => {
  console.log('Add contact');
};

const onEdit = (contact) => {
  console.log('Edit contact:', contact);
};
</script>
```

## Best Practices

1. **Default Contact**: Mark one contact as default using `isDefault` property
2. **User Feedback**: Provide clear feedback when contact is selected or edited
3. **Empty State**: Handle empty list gracefully with appropriate UI
4. **Integration**: Combine with ContactEdit for complete contact management
5. **Performance**: For large lists, consider pagination or virtual scrolling
6. **Data Validation**: Validate contact data before displaying
