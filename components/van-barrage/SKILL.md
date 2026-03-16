---
name: "van-barrage"
description: "Barrage component for displaying scrolling bullet comments over video content. Invoke when user needs to implement danmaku/bullet screen functionality for video players or live streams."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Barrage Component

A component for implementing bullet screen (danmaku) functionality, commonly used in video players to display scrolling comments.

## When to Invoke

Invoke this skill when:
- User needs to implement bullet screen/danmaku functionality
- User wants to display scrolling comments over video content
- User needs to create live stream comment overlays
- User asks about implementing video barrage effects
- User wants controllable animation for text overlays

## Features

- **Auto Play**: Automatic barrage animation on mount
- **Manual Control**: Play/pause barrage programmatically
- **Customizable Rows**: Set the number of text rows
- **Animation Duration**: Configurable animation speed
- **Dynamic Addition**: Add new barrage items dynamically
- **Flexible Positioning**: Customize top spacing and delays

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model | Barrage data | `BarrageItem[]` | - |
| auto-play | Whether to play the bullet screen automatically | `boolean` | `true` |
| rows | The number of lines of text | `number \| string` | `4` |
| top | Spacing between the top of the barrage area, unit `px` | `number \| string` | `10` |
| duration | Text animation duration, unit `ms` | `number \| string` | `4000` |
| delay | Barrage animation delay, unit `ms` | `number` | `300` |

### BarrageItem Type

```ts
interface BarrageItem {
  id: number | string
  text: string
}
```

### Methods

Use ref to get Barrage instance and call instance methods.

| Name | Description | Arguments | Return Value |
|------|-------------|-----------|--------------|
| play | Play barrage | - | - |
| pause | Pause barrage | - | - |

### Slots

| Name | Description |
|------|-------------|
| default | Default slot for video or background content |

### Types

```ts
import type { BarrageProps, BarrageItem, BarrageInstance } from 'vant'
```

## Usage Examples

### Basic Usage

```vue
<template>
  <van-barrage v-model="list">
    <div class="video" style="width: 100%; height: 150px"></div>
  </van-barrage>
  <van-space style="margin-top: 10px">
    <van-button @click="add" type="primary" size="small">Add Barrage</van-button>
  </van-space>
</template>

<script setup>
import { ref } from 'vue'

const defaultList = [
  { id: 100, text: 'Lightweight' },
  { id: 101, text: 'Customizable' },
  { id: 102, text: 'Mobile' },
  { id: 103, text: 'Vue' },
  { id: 104, text: 'Library' },
  { id: 105, text: 'VantUI' },
  { id: 106, text: '666' }
]

const list = ref([...defaultList])

const add = () => {
  list.value.push({ id: Math.random(), text: 'Barrage' })
}
</script>
```

### Video Player Style

```vue
<template>
  <van-barrage v-model="list" ref="barrage" :auto-play="false">
    <div class="video" style="width: 100%; height: 150px"></div>
  </van-barrage>
  <van-space style="margin-top: 10px">
    <van-button @click="add" type="primary" size="small" :disabled="!isPlay">
      Add Barrage
    </van-button>
    <van-button @click="toggle()" size="small">
      {{ isPlay ? 'Pause' : 'Play' }}
    </van-button>
  </van-space>
</template>

<script setup>
import { ref, watch } from 'vue'
import { useToggle } from '@vant/use'

const defaultList = [
  { id: 100, text: 'Lightweight' },
  { id: 101, text: 'Customizable' },
  { id: 102, text: 'Mobile' },
  { id: 103, text: 'Vue' },
  { id: 104, text: 'Library' },
  { id: 105, text: 'VantUI' }
]

const list = ref([...defaultList])
const barrage = ref()
const [isPlay, toggle] = useToggle(false)

const add = () => {
  list.value.push({ id: Math.random(), text: 'Barrage' })
}

watch(isPlay, () => {
  if (isPlay.value) {
    barrage.value?.play()
  } else {
    barrage.value?.pause()
  }
})
</script>
```

### Custom Configuration

```vue
<template>
  <van-barrage 
    v-model="list" 
    :rows="6" 
    :duration="3000"
    :delay="200"
    :top="20"
  >
    <video src="your-video.mp4" style="width: 100%"></video>
  </van-barrage>
</template>

<script setup>
import { ref } from 'vue'

const list = ref([
  { id: 1, text: 'Great video!' },
  { id: 2, text: 'Love it!' },
  { id: 3, text: 'Amazing content' }
])
</script>
```

## Common Issues

### 1. Barrage Not Animating

Ensure `auto-play` is `true` or call `play()` method manually:

```vue
<van-barrage v-model="list" ref="barrage" :auto-play="false" />

<script setup>
import { onMounted, ref } from 'vue'

const barrage = ref()

onMounted(() => {
  barrage.value?.play()
})
</script>
```

### 2. Barrage Items Not Showing

Make sure each item has a unique `id`:

```js
const list = ref([
  { id: 1, text: 'First' },
  { id: 2, text: 'Second' }
])

const addItem = () => {
  list.value.push({ 
    id: Date.now(),
    text: 'New item' 
  })
}
```

### 3. Controlling Animation Speed

Adjust `duration` for faster or slower animation:

```vue
<van-barrage v-model="list" :duration="5000" />
```

## Component Interactions

### With Video Player

```vue
<template>
  <div class="video-container">
    <van-barrage v-model="barrages" :auto-play="isPlaying">
      <video 
        ref="videoRef"
        @play="isPlaying = true"
        @pause="isPlaying = false"
      >
        <source src="video.mp4" type="video/mp4">
      </video>
    </van-barrage>
  </div>
</template>
```

### With Input for Live Comments

```vue
<template>
  <van-barrage v-model="list">
    <div class="video-area"></div>
  </van-barrage>
  
  <van-field 
    v-model="inputText" 
    placeholder="Send a comment..."
    @keyup.enter="sendComment"
  >
    <template #button>
      <van-button size="small" @click="sendComment">Send</van-button>
    </template>
  </van-field>
</template>

<script setup>
import { ref } from 'vue'

const list = ref([])
const inputText = ref('')

const sendComment = () => {
  if (inputText.value.trim()) {
    list.value.push({
      id: Date.now(),
      text: inputText.value
    })
    inputText.value = ''
  }
}
</script>
```

## Best Practices

1. **Unique IDs**: Always use unique IDs for barrage items
2. **Performance**: Limit the number of simultaneous barrage items
3. **Sync with video**: Pause barrage when video is paused
4. **User input**: Sanitize user input before adding to barrage
5. **Row count**: Adjust rows based on video height for optimal visibility
6. **Animation timing**: Balance duration and delay for smooth experience
