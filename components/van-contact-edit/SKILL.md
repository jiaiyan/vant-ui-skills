---
name: "van-contact-edit"
description: "Contact editing component for creating and updating contact information. Invoke when user needs to implement contact management functionality."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant ContactEdit Component

Edit and save contact information with form validation.

## When to Invoke

Invoke this skill when:
- User needs to create a new contact
- User wants to edit existing contact information
- User needs to delete contact functionality
- User wants to set default contact
- User asks about contact form validation
- User needs phone number validation

## Features

- **Contact Management**: Create, update, and delete contacts
- **Form Validation**: Built-in phone number validation
- **Custom Validation**: Support for custom validation functions
- **Default Contact**: Option to set contact as default
- **Loading States**: Loading status for save and delete operations
- **Edit Mode**: Different UI for create and edit modes

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| contact-info | Initial contact information | `ContactEditInfo` | `{}` |
| is-edit | Whether in edit mode | `boolean` | `false` |
| is-saving | Whether to show loading on save button | `boolean` | `false` |
| is-deleting | Whether to show loading on delete button | `boolean` | `false` |
| tel-validator | Custom phone number validator | `(tel: string) => boolean` | - |
| show-set-default | Whether to show default contact switch | `boolean` | `false` |
| set-default-label | Label for default contact switch | `string` | - |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| save | Emitted when save button is clicked | `contactInfo: ContactEditInfo` |
| delete | Emitted when delete button is clicked | `contactInfo: ContactEditInfo` |
| change-default | Emitted when default contact switch changes | `checked: boolean` |

### ContactEditInfo Data Structure

| Key | Description | Type |
|-----|-------------|------|
| name | Contact name | `string` |
| tel | Phone number | `string` |
| isDefault | Whether it's the default contact | `boolean \| undefined` |

### Types

```ts
import type { ContactEditInfo, ContactEditProps } from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-contact-edit
    is-edit
    show-set-default
    :contact-info="editingContact"
    set-default-label="Set as default contact"
    @save="onSave"
    @delete="onDelete"
  />
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const editingContact = ref({
  tel: '',
  name: '',
});

const onSave = (contactInfo) => {
  showToast('Save');
  console.log('Saved contact:', contactInfo);
};

const onDelete = (contactInfo) => {
  showToast('Delete');
  console.log('Deleted contact:', contactInfo);
};
</script>
```

### Create New Contact

```vue
<template>
  <van-contact-edit
    :contact-info="newContact"
    show-set-default
    @save="onSave"
  />
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const newContact = ref({
  name: '',
  tel: '',
  isDefault: false,
});

const onSave = (contactInfo) => {
  showToast('Contact created');
  console.log('New contact:', contactInfo);
};
</script>
```

### Edit Existing Contact

```vue
<template>
  <van-contact-edit
    is-edit
    :contact-info="contact"
    show-set-default
    @save="onSave"
    @delete="onDelete"
  />
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const contact = ref({
  name: 'John Snow',
  tel: '13000000000',
  isDefault: true,
});

const onSave = (info) => {
  showToast('Contact updated');
};

const onDelete = (info) => {
  showToast('Contact deleted');
};
</script>
```

### With Loading States

```vue
<template>
  <van-contact-edit
    is-edit
    :contact-info="contact"
    :is-saving="saving"
    :is-deleting="deleting"
    @save="onSave"
    @delete="onDelete"
  />
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const contact = ref({
  name: 'John Snow',
  tel: '13000000000',
});

const saving = ref(false);
const deleting = ref(false);

const onSave = async (info) => {
  saving.value = true;
  try {
    await saveContact(info);
    showToast('Saved successfully');
  } finally {
    saving.value = false;
  }
};

const onDelete = async (info) => {
  deleting.value = true;
  try {
    await deleteContact(info);
    showToast('Deleted successfully');
  } finally {
    deleting.value = false;
  }
};
</script>
```

### With Custom Phone Validation

```vue
<template>
  <van-contact-edit
    :contact-info="contact"
    :tel-validator="telValidator"
    @save="onSave"
  />
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const contact = ref({
  name: '',
  tel: '',
});

const telValidator = (tel) => {
  return /^1[3-9]\d{9}$/.test(tel);
};

const onSave = (info) => {
  showToast('Contact saved');
};
</script>
```

### With Default Contact Switch

```vue
<template>
  <van-contact-edit
    :contact-info="contact"
    show-set-default
    set-default-label="Set as default contact"
    @save="onSave"
    @change-default="onChangeDefault"
  />
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const contact = ref({
  name: '',
  tel: '',
  isDefault: false,
});

const onChangeDefault = (checked) => {
  console.log('Default contact:', checked);
};

const onSave = (info) => {
  showToast('Contact saved');
};
</script>
```

### Complete Contact Management Flow

```vue
<template>
  <div>
    <van-contact-list
      v-if="!editing"
      v-model="selectedId"
      :list="contactList"
      @add="onAdd"
      @edit="onEdit"
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

const editing = ref(false);
const isEditMode = ref(false);
const selectedId = ref('');
const contactList = ref([
  { id: '1', name: 'John Snow', tel: '13000000000', isDefault: true },
]);

const editingContact = ref({
  name: '',
  tel: '',
  isDefault: false,
});

const onAdd = () => {
  isEditMode.value = false;
  editingContact.value = { name: '', tel: '', isDefault: false };
  editing.value = true;
};

const onEdit = (contact) => {
  isEditMode.value = true;
  editingContact.value = { ...contact };
  editing.value = true;
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
  editing.value = false;
  showToast('Saved');
};

const onDelete = (info) => {
  contactList.value = contactList.value.filter(c => c.id !== selectedId.value);
  editing.value = false;
  showToast('Deleted');
};
</script>
```

## Best Practices

1. **Mode Distinction**: Use `is-edit` to distinguish between create and edit modes
2. **Validation**: Implement `tel-validator` for phone number validation
3. **Loading States**: Show loading indicators during async operations
4. **Default Contact**: Use `show-set-default` for default contact management
5. **User Feedback**: Provide clear feedback after save/delete operations
6. **Data Binding**: Pre-fill `contact-info` when editing existing contacts
7. **Form Reset**: Reset form data after successful save or cancel
