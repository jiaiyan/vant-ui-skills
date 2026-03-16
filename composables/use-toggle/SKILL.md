---
name: "use-toggle"
description: "Composable for toggling boolean state. Invoke when implementing switches, checkboxes, modals, or any UI that needs to toggle between true and false."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# useToggle

A Vue 3 composable for toggling between `true` and `false` states, providing a simple way to manage boolean state.

## When to Invoke

Invoke this skill when:
- User needs to toggle a boolean state
- User wants to implement a simple on/off switch
- User needs to show/hide elements
- User wants to manage modal or dialog visibility
- User needs to implement expand/collapse functionality

## Features

- **Simple API**: Returns state and toggle function as array
- **Default Value**: Supports custom default value
- **Explicit Toggle**: Can set explicit true/false values
- **Reactive**: State is a reactive ref
- **TypeScript Support**: Full TypeScript type definitions

## API Reference

### Type Declarations

```ts
function useToggle(
  defaultValue: boolean,
): [Ref<boolean>, (newValue?: boolean) => void];
```

### Parameters

| Name | Description | Type | Default Value |
| --- | --- | --- | --- |
| defaultValue | Initial boolean value | `boolean` | `false` |

### Return Value

| Name | Description | Type |
| --- | --- | --- |
| state | Current boolean state | `Ref<boolean>` |
| toggle | Function to toggle or set state | `(newValue?: boolean) => void` |

## Usage Examples

### Basic Usage

```vue
<template>
  <div>
    <p>State: {{ state }}</p>
    <button @click="toggle()">Toggle</button>
  </div>
</template>

<script setup>
import { useToggle } from '@vant/use';

const [state, toggle] = useToggle();

toggle(true);
console.log(state.value);

toggle(false);
console.log(state.value);

toggle();
console.log(state.value);
</script>
```

### Modal Visibility

```vue
<template>
  <div>
    <button @click="toggleModal(true)">Open Modal</button>
    
    <div v-if="isModalOpen" class="modal">
      <div class="modal-content">
        <h2>Modal Title</h2>
        <p>Modal content here</p>
        <button @click="toggleModal(false)">Close</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { useToggle } from '@vant/use';

const [isModalOpen, toggleModal] = useToggle(false);
</script>

<style scoped>
.modal {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal-content {
  background: white;
  padding: 24px;
  border-radius: 8px;
  max-width: 400px;
}
</style>
```

### Expand/Collapse Panel

```vue
<template>
  <div class="panel">
    <div class="header" @click="toggleExpanded()">
      <span>{{ expanded ? '▼' : '▶' }}</span>
      <span>Click to {{ expanded ? 'collapse' : 'expand' }}</span>
    </div>
    <div v-show="expanded" class="content">
      <p>Hidden content that can be expanded or collapsed.</p>
    </div>
  </div>
</template>

<script setup>
import { useToggle } from '@vant/use';

const [expanded, toggleExpanded] = useToggle(false);
</script>

<style scoped>
.panel {
  border: 1px solid #ddd;
  border-radius: 4px;
}

.header {
  padding: 12px;
  cursor: pointer;
  background: #f5f5f5;
  display: flex;
  gap: 8px;
}

.content {
  padding: 16px;
}
</style>
```

### Password Visibility Toggle

```vue
<template>
  <div class="password-field">
    <input 
      :type="showPassword ? 'text' : 'password'" 
      v-model="password"
      placeholder="Enter password"
    />
    <button @click="togglePassword()">
      {{ showPassword ? '🙈' : '👁️' }}
    </button>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useToggle } from '@vant/use';

const password = ref('');
const [showPassword, togglePassword] = useToggle(false);
</script>

<style scoped>
.password-field {
  display: flex;
  gap: 8px;
}

.password-field input {
  flex: 1;
  padding: 8px 12px;
}

.password-field button {
  padding: 8px 12px;
  background: none;
  border: 1px solid #ddd;
  cursor: pointer;
}
</style>
```

### Sidebar Toggle

```vue
<template>
  <div class="layout">
    <aside :class="{ open: isSidebarOpen }">
      <nav>
        <a href="#">Home</a>
        <a href="#">About</a>
        <a href="#">Contact</a>
      </nav>
    </aside>
    <main>
      <button @click="toggleSidebar()">
        {{ isSidebarOpen ? 'Close' : 'Open' }} Sidebar
      </button>
      <p>Main content area</p>
    </main>
  </div>
</template>

<script setup>
import { useToggle } from '@vant/use';

const [isSidebarOpen, toggleSidebar] = useToggle(true);
</script>

<style scoped>
.layout {
  display: flex;
  min-height: 100vh;
}

aside {
  width: 250px;
  background: #333;
  color: white;
  padding: 16px;
  transform: translateX(-100%);
  transition: transform 0.3s;
}

aside.open {
  transform: translateX(0);
}

aside nav {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

aside nav a {
  color: white;
  text-decoration: none;
  padding: 8px;
}

main {
  flex: 1;
  padding: 16px;
}
</style>
```

### Multiple Toggles

```vue
<template>
  <div class="settings">
    <div class="setting-item">
      <span>Dark Mode</span>
      <button @click="toggleDarkMode()">
        {{ darkMode ? '🌙' : '☀️' }}
      </button>
    </div>
    <div class="setting-item">
      <span>Notifications</span>
      <button @click="toggleNotifications()">
        {{ notifications ? '🔔' : '🔕' }}
      </button>
    </div>
    <div class="setting-item">
      <span>Auto-save</span>
      <button @click="toggleAutoSave()">
        {{ autoSave ? '✓' : '✗' }}
      </button>
    </div>
  </div>
</template>

<script setup>
import { useToggle } from '@vant/use';

const [darkMode, toggleDarkMode] = useToggle(false);
const [notifications, toggleNotifications] = useToggle(true);
const [autoSave, toggleAutoSave] = useToggle(true);
</script>

<style scoped>
.settings {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.setting-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px;
  background: #f5f5f5;
  border-radius: 4px;
}

.setting-item button {
  padding: 8px 16px;
  border: none;
  background: #409eff;
  color: white;
  border-radius: 4px;
  cursor: pointer;
}
</style>
```

### Toggle with Default True

```vue
<template>
  <div>
    <p>Feature is {{ enabled ? 'enabled' : 'disabled' }}</p>
    <button @click="toggle()">
      {{ enabled ? 'Disable' : 'Enable' }}
    </button>
  </div>
</template>

<script setup>
import { useToggle } from '@vant/use';

const [enabled, toggle] = useToggle(true);
</script>
```

### Conditional Toggle

```vue
<template>
  <div>
    <p>Status: {{ isActive ? 'Active' : 'Inactive' }}</p>
    <button @click="handleToggle">
      Toggle (only when allowed)
    </button>
    <label>
      <input type="checkbox" v-model="allowToggle" />
      Allow toggle
    </label>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useToggle } from '@vant/use';

const [isActive, toggle] = useToggle(false);
const allowToggle = ref(true);

const handleToggle = () => {
  if (allowToggle.value) {
    toggle();
  } else {
    alert('Toggle is not allowed!');
  }
};
</script>
```

## Best Practices

1. **Default Value**: Set appropriate default based on use case
2. **Explicit Toggle**: Use `toggle(true)` or `toggle(false)` for explicit control
3. **Destructuring**: Use array destructuring for cleaner code
4. **Naming**: Name the toggle function descriptively (e.g., `toggleModal`)
5. **Combine with v-model**: Can be used with v-model for form controls
