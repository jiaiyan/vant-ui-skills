---
name: "van-count-down"
description: "Countdown component for displaying real-time countdown values. Invoke when user needs to implement countdown timers, time-limited activities, or time displays."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant CountDown Component

Used to display the countdown value in real time, and precision supports milliseconds.

## When to Invoke

Invoke this skill when:
- User needs to implement countdown timers
- User wants to show time-limited promotions or activities
- User needs to display remaining time with custom format
- User wants to control countdown manually (start, pause, reset)
- User asks about millisecond precision countdown

## Features

- **Real-time Updates**: Automatic countdown with configurable precision
- **Custom Format**: Flexible time format with multiple placeholders
- **Millisecond Support**: Support millisecond-level precision
- **Manual Control**: Start, pause, and reset methods
- **Auto Start**: Configurable auto-start behavior
- **Custom Styling**: Full control over countdown display via slots

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| time | Total time, unit milliseconds | `number \| string` | `0` |
| format | Time format | `string` | `HH:mm:ss` |
| auto-start | Whether to auto start count down | `boolean` | `true` |
| millisecond | Whether to enable millisecond render | `boolean` | `false` |

### Available Formats

| Format | Description |
|--------|-------------|
| DD | Day |
| HH | Hour |
| mm | Minute |
| ss | Second |
| S | Millisecond, 1-digit |
| SS | Millisecond, 2-digits |
| SSS | Millisecond, 3-digits |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| finish | Emitted when count down finished | - |
| change | Emitted when count down changed | `currentTime: CurrentTime` |

### Slots

| Name | Description | SlotProps |
|------|-------------|-----------|
| default | Custom Content | `currentTime: CurrentTime` |

### CurrentTime Structure

| Name | Description | Type |
|------|-------------|------|
| total | Total time, unit milliseconds | `number` |
| days | Remain days | `number` |
| hours | Remain hours | `number` |
| minutes | Remain minutes | `number` |
| seconds | Remain seconds | `number` |
| milliseconds | Remain milliseconds | `number` |

### Methods

| Name | Description | Attribute | Return value |
|------|-------------|-----------|--------------|
| start | Start count down | - | - |
| pause | Pause count down | - | - |
| reset | Reset count down | - | - |

### Types

```ts
import type {
  CountDownProps,
  CountDownInstance,
  CountDownCurrentTime,
} from 'vant';
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-count-down :time="time" />
</template>

<script setup>
import { ref } from 'vue';

const time = ref(30 * 60 * 60 * 1000);
</script>
```

### Custom Format

```vue
<template>
  <van-count-down :time="time" format="DD Day, HH:mm:ss" />
</template>

<script setup>
import { ref } from 'vue';

const time = ref(30 * 60 * 60 * 1000);
</script>
```

### Millisecond Precision

```vue
<template>
  <van-count-down millisecond :time="time" format="HH:mm:ss:SS" />
</template>

<script setup>
import { ref } from 'vue';

const time = ref(30 * 60 * 60 * 1000);
</script>
```

### Custom Style

```vue
<template>
  <van-count-down :time="time">
    <template #default="timeData">
      <span class="block">{{ timeData.hours }}</span>
      <span class="colon">:</span>
      <span class="block">{{ timeData.minutes }}</span>
      <span class="colon">:</span>
      <span class="block">{{ timeData.seconds }}</span>
    </template>
  </van-count-down>
</template>

<style scoped>
.colon {
  display: inline-block;
  margin: 0 4px;
  color: #1989fa;
}

.block {
  display: inline-block;
  width: 22px;
  color: #fff;
  font-size: 12px;
  text-align: center;
  background-color: #1989fa;
}
</style>
```

### Manual Control

```vue
<template>
  <van-count-down
    ref="countDown"
    millisecond
    :time="3000"
    :auto-start="false"
    format="ss:SSS"
    @finish="onFinish"
  />
  <van-grid clickable :column-num="3">
    <van-grid-item text="Start" icon="play-circle-o" @click="start" />
    <van-grid-item text="Pause" icon="pause-circle-o" @click="pause" />
    <van-grid-item text="Reset" icon="replay" @click="reset" />
  </van-grid>
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';

const countDown = ref(null);

const start = () => {
  countDown.value.start();
};

const pause = () => {
  countDown.value.pause();
};

const reset = () => {
  countDown.value.reset();
};

const onFinish = () => showToast('Finished');
</script>
```

### With Days

```vue
<template>
  <van-count-down :time="time">
    <template #default="timeData">
      <span v-if="timeData.days > 0">
        {{ timeData.days }} days 
      </span>
      <span>{{ timeData.hours }}:{{ timeData.minutes }}:{{ timeData.seconds }}</span>
    </template>
  </van-count-down>
</template>

<script setup>
import { ref } from 'vue';

const time = ref(3 * 24 * 60 * 60 * 1000);
</script>
```

## Common Issues

### 1. Countdown Not Starting

Make sure `auto-start` is not set to `false`, or call `start()` method manually:

```vue
<template>
  <van-count-down ref="countDown" :time="time" :auto-start="false" />
  <van-button @click="countDown.start()">Start</van-button>
</template>
```

### 2. Format Not Working

Ensure format placeholders are uppercase:

```vue
<van-count-down :time="time" format="HH:mm:ss" />
```

### 3. Reset Not Working

After reset, you need to call `start()` to begin countdown again:

```vue
<script setup>
const resetAndStart = () => {
  countDown.value.reset();
  countDown.value.start();
};
</script>
```

## Component Interactions

### With Promotion Banner

```vue
<template>
  <div class="promotion-banner">
    <h3>Flash Sale Ends In:</h3>
    <van-count-down :time="remainingTime" @finish="onSaleEnd">
      <template #default="timeData">
        <span class="time-block">{{ timeData.hours }}</span>
        <span class="separator">:</span>
        <span class="time-block">{{ timeData.minutes }}</span>
        <span class="separator">:</span>
        <span class="time-block">{{ timeData.seconds }}</span>
      </template>
    </van-count-down>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const remainingTime = ref(0);

onMounted(() => {
  const endTime = new Date('2024-12-31 23:59:59').getTime();
  remainingTime.value = endTime - Date.now();
});

const onSaleEnd = () => {
  console.log('Sale ended');
};
</script>
```

### With Verification Code

```vue
<template>
  <van-field v-model="code" label="Code">
    <template #button>
      <van-button 
        size="small" 
        :disabled="counting"
        @click="sendCode"
      >
        <van-count-down 
          v-if="counting"
          ref="countDown"
          :time="60000"
          :auto-start="false"
          format="ss s"
          @finish="onCountFinish"
        />
        <span v-else>Send Code</span>
      </van-button>
    </template>
  </van-field>
</template>

<script setup>
import { ref } from 'vue';

const code = ref('');
const counting = ref(false);
const countDown = ref(null);

const sendCode = () => {
  counting.value = true;
  countDown.value.start();
};

const onCountFinish = () => {
  counting.value = false;
};
</script>
```

## Best Practices

1. **Use appropriate precision**: Only enable millisecond when necessary for performance
2. **Provide clear feedback**: Show finish event to users when countdown completes
3. **Handle edge cases**: Consider what happens when time reaches zero
4. **Custom styling**: Use slots for better visual presentation
5. **Accessibility**: Ensure countdown is accessible to screen readers
