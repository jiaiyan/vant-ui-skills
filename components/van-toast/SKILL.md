---
name: "van-toast"
description: "Toast component for displaying message notifications, loading hints, and operation results. Invoke when user needs to show feedback messages or loading states."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Toast Component

Black semi-transparent pop-up hint in the middle of the page, used for message notification, loading hint, operation result hint and other scenarios.

## When to Invoke

Invoke this skill when:
- User needs to show a message notification
- User wants to display a loading indicator
- User needs to show success or failure feedback
- User wants to create custom toast messages
- User asks about toast positioning or duration

## Features

- **Multiple Types**: Text, loading, success, fail, and custom HTML
- **Position Options**: Top, middle, bottom
- **Custom Icons**: Support for custom icons and images
- **Loading Types**: Circular and spinner loading animations
- **Singleton Mode**: Only one toast at a time by default
- **Multiple Mode**: Support for multiple toasts simultaneously
- **Global Configuration**: Set default options for all toasts

## API Reference

### Methods

| Name | Description | Attribute | Return value |
|------|-------------|-----------|--------------|
| showToast | Display a text toast | `ToastOptions \| string` | Toast instance |
| showLoadingToast | Display a loading toast | `ToastOptions \| string` | Toast instance |
| showSuccessToast | Display a success toast | `ToastOptions \| string` | Toast instance |
| showFailToast | Display a fail toast | `ToastOptions \| string` | Toast instance |
| closeToast | Close the currently displayed toast | `closeAll: boolean` | `void` |
| allowMultipleToast | Allow multiple toasts at the same time | - | `void` |
| setToastDefaultOptions | Modify default configuration | `type \| ToastOptions` | `void` |
| resetToastDefaultOptions | Reset default configuration | `type` | `void` |

### ToastOptions

| Name | Description | Type | Default |
|------|-------------|------|---------|
| type | Toast type: `loading` `success` `fail` `html` | `ToastType` | `text` |
| position | Toast position: `top` `middle` `bottom` | `ToastPosition` | `middle` |
| message | Message content | `string` | `''` |
| wordBreak | Word break mode: `normal` `break-all` `break-word` | `ToastWordBreak` | `'break-all'` |
| icon | Custom icon name or image URL | `string` | - |
| iconSize | Custom icon size | `number \| string` | `36px` |
| iconPrefix | Icon className prefix | `string` | `van-icon` |
| overlay | Whether to show overlay | `boolean` | `false` |
| forbidClick | Whether to forbid background clicks | `boolean` | `false` |
| closeOnClick | Whether to close after clicked | `boolean` | `false` |
| closeOnClickOverlay | Whether to close when overlay is clicked | `boolean` | `false` |
| loadingType | Loading icon type: `circular` `spinner` | `string` | `circular` |
| duration | Toast duration (ms), 0 for persistent | `number` | `2000` |
| className | Custom className | `string \| Array \| object` | - |
| overlayClass | Custom overlay class | `string \| Array \| object` | - |
| overlayStyle | Custom overlay style | `object` | - |
| transition | Transition name | `string` | `van-fade` |
| teleport | Target element where Toast will be mounted | `string \| Element` | `body` |
| zIndex | Set z-index to a fixed value | `number \| string` | `2000+` |
| onClose | Callback after close | `Function` | - |
| onOpened | Callback after opened | `Function` | - |

### Props (Component Usage)

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model:show | Whether to show toast | `boolean` | `false` |
| type | Toast type | `ToastType` | `text` |
| position | Toast position | `ToastPosition` | `middle` |
| message | Message content | `string` | `''` |
| word-break | Word break mode | `ToastWordBreak` | `'break-all'` |
| icon | Custom icon | `string` | - |
| icon-size | Custom icon size | `number \| string` | `36px` |
| icon-prefix | Icon className prefix | `string` | `van-icon` |
| overlay | Whether to show overlay | `boolean` | `false` |
| forbid-click | Whether to forbid background clicks | `boolean` | `false` |
| close-on-click | Whether to close after clicked | `boolean` | `false` |
| close-on-click-overlay | Whether to close when overlay is clicked | `boolean` | `false` |
| loading-type | Loading icon type | `string` | `circular` |
| duration | Toast duration (ms) | `number` | `2000` |
| class-name | Custom className | `string \| Array \| object` | - |
| overlay-class | Custom overlay class | `string \| Array \| object` | - |
| overlay-style | Custom overlay style | `object` | - |
| transition | Transition name | `string` | `van-fade` |
| teleport | Target element | `string \| Element` | `body` |
| z-index | Set z-index | `number \| string` | `2000+` |

### Events (Component Usage)

| Event | Description | Parameters |
|-------|-------------|------------|
| close | Callback after close | - |
| opened | Callback after opened | - |

### Slots

| Name | Description |
|------|-------------|
| message | Custom message content |

### Types

```ts
import type {
  ToastType,
  ToastProps,
  ToastOptions,
  ToastPosition,
  ToastWordBreak,
  ToastWrapperInstance,
} from 'vant';
```

## Usage Examples

### Text Toast

```vue
<template>
  <van-button @click="showTextToast">Show Text Toast</van-button>
</template>

<script setup>
import { showToast } from 'vant';

const showTextToast = () => {
  showToast('Some messages');
};
</script>
```

### Loading Toast

```vue
<template>
  <van-button @click="showLoading">Show Loading</van-button>
</template>

<script setup>
import { showLoadingToast, closeToast } from 'vant';

const showLoading = () => {
  showLoadingToast({
    message: 'Loading...',
    forbidClick: true,
  });
  
  setTimeout(() => {
    closeToast();
  }, 2000);
};
</script>
```

### Success/Fail Toast

```vue
<template>
  <van-button @click="showSuccess">Success</van-button>
  <van-button @click="showFail">Fail</van-button>
</template>

<script setup>
import { showSuccessToast, showFailToast } from 'vant';

const showSuccess = () => {
  showSuccessToast('Success');
};

const showFail = () => {
  showFailToast('Fail');
};
</script>
```

### Custom Icon

```vue
<template>
  <van-button @click="showCustomIcon">Custom Icon</van-button>
  <van-button @click="showCustomImage">Custom Image</van-button>
</template>

<script setup>
import { showToast, showLoadingToast } from 'vant';

const showCustomIcon = () => {
  showToast({
    message: 'Custom Icon',
    icon: 'like-o',
  });
};

const showCustomImage = () => {
  showToast({
    message: 'Custom Image',
    icon: 'https://fastly.jsdelivr.net/npm/@vant/assets/logo.png',
  });
};
</script>
```

### Loading Type

```vue
<template>
  <van-button @click="showSpinner">Spinner Loading</van-button>
</template>

<script setup>
import { showLoadingToast } from 'vant';

const showSpinner = () => {
  showLoadingToast({
    message: 'Loading...',
    forbidClick: true,
    loadingType: 'spinner',
  });
};
</script>
```

### Custom Position

```vue
<template>
  <van-button @click="showTop">Top</van-button>
  <van-button @click="showBottom">Bottom</van-button>
</template>

<script setup>
import { showToast } from 'vant';

const showTop = () => {
  showToast({
    message: 'Top',
    position: 'top',
  });
};

const showBottom = () => {
  showToast({
    message: 'Bottom',
    position: 'bottom',
  });
};
</script>
```

### Update Message

```vue
<template>
  <van-button @click="startCountdown">Start Countdown</van-button>
</template>

<script setup>
import { showLoadingToast, closeToast } from 'vant';

const startCountdown = () => {
  const toast = showLoadingToast({
    duration: 0,
    forbidClick: true,
    loadingType: 'spinner',
    message: '3 seconds',
  });

  let second = 3;
  const timer = setInterval(() => {
    second--;
    if (second) {
      toast.message = `${second} seconds`;
    } else {
      clearInterval(timer);
      closeToast();
    }
  }, 1000);
};
</script>
```

### Multiple Toasts

```vue
<template>
  <van-button @click="showMultiple">Show Multiple</van-button>
</template>

<script setup>
import { showToast, showSuccessToast, allowMultipleToast } from 'vant';

const showMultiple = () => {
  allowMultipleToast();

  const toast1 = showToast('First Toast');
  const toast2 = showSuccessToast('Second Toast');

  setTimeout(() => {
    toast1.close();
    toast2.close();
  }, 2000);
};
</script>
```

### Set Default Options

```vue
<template>
  <van-button @click="setDefaults">Set Defaults</van-button>
  <van-button @click="resetDefaults">Reset Defaults</van-button>
</template>

<script setup>
import { setToastDefaultOptions, resetToastDefaultOptions } from 'vant';

const setDefaults = () => {
  setToastDefaultOptions({ duration: 2000 });
  setToastDefaultOptions('loading', { forbidClick: true });
};

const resetDefaults = () => {
  resetToastDefaultOptions();
  resetToastDefaultOptions('loading');
};
</script>
```

### Component Usage

```vue
<template>
  <van-button @click="show = true">Show Toast Component</van-button>
  <van-toast v-model:show="show" style="padding: 0">
    <template #message>
      <van-image :src="image" width="200" height="140" style="display: block" />
    </template>
  </van-toast>
</template>

<script setup>
import { ref } from 'vue';

const show = ref(false);
const image = 'https://fastly.jsdelivr.net/npm/@vant/assets/logo.png';
</script>
```

### Async Operation

```vue
<template>
  <van-button @click="submitForm" :loading="submitting">Submit</van-button>
</template>

<script setup>
import { ref } from 'vue';
import { showLoadingToast, showSuccessToast, closeToast } from 'vant';

const submitting = ref(false);

const submitForm = async () => {
  submitting.value = true;
  showLoadingToast({
    message: 'Submitting...',
    forbidClick: true,
    duration: 0,
  });

  try {
    await new Promise(resolve => setTimeout(resolve, 2000));
    closeToast();
    showSuccessToast('Submit success');
  } catch (error) {
    closeToast();
    showSuccessToast('Submit failed');
  } finally {
    submitting.value = false;
  }
};
</script>
```

### Form Validation

```vue
<template>
  <van-form @submit="onSubmit">
    <van-field v-model="username" name="username" label="Username" />
    <van-field v-model="password" type="password" name="password" label="Password" />
    <div style="margin: 16px;">
      <van-button round block type="primary" native-type="submit">
        Submit
      </van-button>
    </div>
  </van-form>
</template>

<script setup>
import { ref } from 'vue';
import { showToast, showLoadingToast, showSuccessToast, closeToast } from 'vant';

const username = ref('');
const password = ref('');

const onSubmit = async () => {
  if (!username.value || !password.value) {
    showToast('Please fill in all fields');
    return;
  }

  showLoadingToast({
    message: 'Logging in...',
    forbidClick: true,
    duration: 0,
  });

  await new Promise(resolve => setTimeout(resolve, 1500));
  closeToast();
  showSuccessToast('Login success');
};
</script>
```

## Best Practices

1. **Use appropriate type**: Use success/fail for results, loading for async operations
2. **Set forbidClick**: Enable `forbidClick` for loading states to prevent double submission
3. **Proper duration**: Use 0 for persistent toasts and close manually
4. **Position**: Use `top` or `bottom` for important messages that shouldn't be missed
5. **Close properly**: Always close loading toasts after async operations complete
6. **Avoid explicit import**: When using auto-import, don't explicitly import toast functions
