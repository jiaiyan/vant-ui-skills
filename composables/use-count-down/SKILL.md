---
name: "use-count-down"
description: "Composable for managing countdown timers. Invoke when implementing countdown displays, verification code timers, or any time-based countdown functionality."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# useCountDown

A Vue 3 composable for managing countdown timers with support for days, hours, minutes, seconds, and milliseconds.

## When to Invoke

Invoke this skill when:
- User needs to implement a countdown timer
- User wants to show remaining time for verification codes
- User needs to display countdown for flash sales or limited-time offers
- User wants to track time remaining with millisecond precision
- User needs to start, pause, or reset a countdown

## Features

- **Granular Time Display**: Provides days, hours, minutes, seconds, and milliseconds
- **Millisecond Rendering**: Optional high-precision rendering mode
- **Control Methods**: Start, pause, and reset functionality
- **Event Callbacks**: onChange and onFinish callbacks
- **Reactive State**: Current time is a computed ref that updates automatically
- **TypeScript Support**: Full TypeScript type definitions

## API Reference

### Type Declarations

```ts
type CurrentTime = {
  days: number;
  hours: number;
  total: number;
  minutes: number;
  seconds: number;
  milliseconds: number;
};

type CountDown = {
  start: () => void;
  pause: () => void;
  reset: (totalTime?: number) => void;
  current: ComputedRef<CurrentTime>;
};

type UseCountDownOptions = {
  time: number;
  millisecond?: boolean;
  onChange?: (current: CurrentTime) => void;
  onFinish?: () => void;
};

function useCountDown(options: UseCountDownOptions): CountDown;
```

### Options

| Name | Description | Type | Default Value |
| --- | --- | --- | --- |
| time | Total countdown time in milliseconds | `number` | - |
| millisecond | Enable millisecond rendering | `boolean` | `false` |
| onChange | Callback when countdown changes | `(current: CurrentTime) => void` | - |
| onFinish | Callback when countdown finishes | `() => void` | - |

### Return Value

| Name | Description | Type |
| --- | --- | --- |
| current | Current remaining time object | `ComputedRef<CurrentTime>` |
| start | Start the countdown | `() => void` |
| pause | Pause the countdown | `() => void` |
| reset | Reset the countdown (optionally with new time) | `(time?: number) => void` |

### CurrentTime Structure

| Name | Description | Type |
| --- | --- | --- |
| total | Total remaining time in milliseconds | `number` |
| days | Remaining days | `number` |
| hours | Remaining hours | `number` |
| minutes | Remaining minutes | `number` |
| seconds | Remaining seconds | `number` |
| milliseconds | Remaining milliseconds | `number` |

## Usage Examples

### Basic Usage

```vue
<template>
  <div class="countdown">
    <p>Days: {{ current.days }}</p>
    <p>Hours: {{ current.hours }}</p>
    <p>Minutes: {{ current.minutes }}</p>
    <p>Seconds: {{ current.seconds }}</p>
    <p>Total: {{ current.total }}ms</p>
  </div>
</template>

<script setup>
import { useCountDown } from '@vant/use';

const countDown = useCountDown({
  time: 24 * 60 * 60 * 1000,
});

countDown.start();

const { current } = countDown;
</script>
```

### Verification Code Timer

```vue
<template>
  <div class="verification">
    <input v-model="code" placeholder="Enter code" />
    <button 
      :disabled="counting" 
      @click="sendCode"
    >
      {{ counting ? `${current.seconds}s` : 'Send Code' }}
    </button>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useCountDown } from '@vant/use';

const code = ref('');
const counting = ref(false);

const countDown = useCountDown({
  time: 60 * 1000,
  onFinish: () => {
    counting.value = false;
  },
});

const { current, start } = countDown;

const sendCode = () => {
  counting.value = true;
  start();
};
</script>
```

### Millisecond Precision

```vue
<template>
  <div class="precision-countdown">
    <p>{{ formattedTime }}</p>
  </div>
</template>

<script setup>
import { computed } from 'vue';
import { useCountDown } from '@vant/use';

const countDown = useCountDown({
  time: 10 * 1000,
  millisecond: true,
  onFinish: () => {
    console.log('Countdown finished!');
  },
});

countDown.start();

const { current } = countDown;

const formattedTime = computed(() => {
  const { seconds, milliseconds } = current.value;
  return `${seconds}.${String(milliseconds).padStart(3, '0')}s`;
});
</script>
```

### Flash Sale Countdown

```vue
<template>
  <div class="flash-sale">
    <h3>Flash Sale Ends In:</h3>
    <div class="time-blocks">
      <div class="block">
        <span class="number">{{ current.hours }}</span>
        <span class="label">Hours</span>
      </div>
      <div class="block">
        <span class="number">{{ current.minutes }}</span>
        <span class="label">Minutes</span>
      </div>
      <div class="block">
        <span class="number">{{ current.seconds }}</span>
        <span class="label">Seconds</span>
      </div>
    </div>
    <div class="controls">
      <button @click="pause">Pause</button>
      <button @click="start">Resume</button>
      <button @click="reset(2 * 60 * 60 * 1000)">Reset (2h)</button>
    </div>
  </div>
</template>

<script setup>
import { useCountDown } from '@vant/use';

const countDown = useCountDown({
  time: 2 * 60 * 60 * 1000,
  onChange: (current) => {
    console.log('Time remaining:', current.total);
  },
  onFinish: () => {
    alert('Flash sale has ended!');
  },
});

const { current, start, pause, reset } = countDown;
</script>

<style scoped>
.time-blocks {
  display: flex;
  gap: 10px;
}

.block {
  text-align: center;
}

.number {
  display: block;
  font-size: 24px;
  font-weight: bold;
}

.label {
  font-size: 12px;
  color: #666;
}
</style>
```

### With Pause and Reset

```vue
<template>
  <div class="timer">
    <p>{{ current.minutes }}:{{ String(current.seconds).padStart(2, '0') }}</p>
    <button @click="start">Start</button>
    <button @click="pause">Pause</button>
    <button @click="reset()">Reset</button>
  </div>
</template>

<script setup>
import { useCountDown } from '@vant/use';

const countDown = useCountDown({
  time: 5 * 60 * 1000,
});

const { current, start, pause, reset } = countDown;
</script>
```

## Best Practices

1. **Start Manually**: Always call `start()` to begin the countdown
2. **Cleanup**: The countdown automatically pauses when component unmounts
3. **Millisecond Mode**: Only enable when needed for performance
4. **Reset with New Time**: Pass a new time value to `reset()` to change duration
5. **Event Handling**: Use `onFinish` for post-countdown actions
