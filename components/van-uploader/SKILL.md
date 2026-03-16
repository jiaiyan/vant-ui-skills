---
name: "van-uploader"
description: "Uploader component for file uploads with preview and progress. Invoke when user needs to implement file uploads, image uploads, or document uploads."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Uploader Component

Uploader component for uploading files with preview, progress, and status management.

## When to Invoke

Invoke this skill when:
- User needs to implement file upload functionality
- User wants to create image upload with preview
- User needs to limit file size or count
- User wants to customize upload appearance
- User asks about upload status and progress

## Features

- **File Preview**: Preview images and files before upload
- **Multiple Upload**: Support for multiple file selection
- **Size Limit**: Configurable maximum file size
- **Count Limit**: Limit number of files
- **Upload Status**: Show uploading, success, and failed states
- **Custom Upload Area**: Customizable upload button
- **Before Read**: Pre-processing and validation hooks
- **After Read**: Post-processing hooks
- **Reupload**: Support for re-uploading files
- **Preview Cover**: Custom preview overlay content

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| v-model | List of uploaded files | `FileListItem[]` | - |
| accept | Accepted file type | `string` | `image/*` |
| name | Input name | `number \| string` | - |
| preview-size | Size of preview image | `number \| string \| Array` | `80px` |
| preview-image | Whether to show image preview | `boolean` | `true` |
| preview-full-image | Whether to show full screen image preview | `boolean` | `true` |
| preview-options | Options of full screen image preview | `object` | - |
| multiple | Whether to enable multiple selection | `boolean` | `false` |
| disabled | Whether to disabled the upload | `boolean` | `false` |
| readonly | Whether to make upload area readonly | `boolean` | `false` |
| deletable | Whether to show delete icon | `boolean` | `true` |
| reupload | Whether to enable reupload | `boolean` | `false` |
| show-upload | Whether to show upload area | `boolean` | `true` |
| lazy-load | Whether to enable lazy load | `boolean` | `false` |
| capture | Capture, can be set to `camera` | `string` | - |
| after-read | Hook after reading the file | `Function` | - |
| before-read | Hook before reading the file | `Function` | - |
| before-delete | Hook before delete the file | `Function` | - |
| max-size | Max size of file | `number \| string \| (file: File) => boolean` | `Infinity` |
| max-count | Max count of image | `number \| string` | `Infinity` |
| result-type | Type of file read result | `string` | `dataUrl` |
| upload-text | Upload text | `string` | - |
| image-fit | Preview image fit mode | `string` | `cover` |
| upload-icon | Upload icon | `string` | `photograph` |

### Events

| Event | Description | Arguments |
|-------|-------------|-----------|
| oversize | Emitted when file size over limit | Same as after-read |
| click-upload | Emitted when click upload area | `event: MouseEvent` |
| click-preview | Emitted when preview image is clicked | Same as after-read |
| click-reupload | Emitted when reupload image is clicked | Same as after-read |
| close-preview | Emitted when the full screen image preview is closed | - |
| delete | Emitted when preview file is deleted | Same as after-read |

### Slots

| Name | Description | SlotProps |
|------|-------------|-----------|
| default | Custom upload area | - |
| preview-delete | Custom delete icon | - |
| preview-cover | Custom content that covers the image preview | `item: FileListItem` |

### Methods

| Name | Description | Attribute | Return value |
|------|-------------|-----------|--------------|
| closeImagePreview | Close full screen image preview | - | - |
| chooseFile | Trigger choosing files | - | - |
| reuploadFile | Trigger choosing files for reupload | `index: number` | - |

## Usage Examples

### Basic Usage

```vue
<template>
  <van-uploader :after-read="afterRead" />
</template>

<script setup>
const afterRead = (file) => {
  console.log(file)
}
</script>
```

### Preview File

```vue
<template>
  <van-uploader v-model="fileList" multiple />
</template>

<script setup>
import { ref } from 'vue'

const fileList = ref([
  { url: 'https://fastly.jsdelivr.net/npm/@vant/assets/leaf.jpeg' },
  { url: 'https://cloud-image', isImage: true }
])
</script>
```

### Upload Status

```vue
<template>
  <van-uploader v-model="fileList" :after-read="afterRead" />
</template>

<script setup>
import { ref } from 'vue'

const fileList = ref([
  {
    url: 'https://fastly.jsdelivr.net/npm/@vant/assets/leaf.jpeg',
    status: 'uploading',
    message: 'Uploading...'
  },
  {
    url: 'https://fastly.jsdelivr.net/npm/@vant/assets/tree.jpeg',
    status: 'failed',
    message: 'Failed'
  }
])

const afterRead = (file) => {
  file.status = 'uploading'
  file.message = 'Uploading...'

  setTimeout(() => {
    file.status = 'failed'
    file.message = 'Failed'
  }, 1000)
}
</script>
```

### Max Count

```vue
<template>
  <van-uploader v-model="fileList" multiple :max-count="2" />
</template>

<script setup>
import { ref } from 'vue'

const fileList = ref([])
</script>
```

### Max Size

```vue
<template>
  <van-uploader 
    multiple 
    :max-size="500 * 1024" 
    @oversize="onOversize" 
  />
</template>

<script setup>
import { showToast } from 'vant'

const onOversize = (file) => {
  console.log(file)
  showToast('File size cannot exceed 500kb')
}
</script>
```

### Custom Size Limit by Type

```vue
<template>
  <van-uploader multiple :max-size="isOverSize" />
</template>

<script setup>
const isOverSize = (file) => {
  const maxSize = file.type === 'image/jpeg' ? 500 * 1024 : 1000 * 1024
  return file.size >= maxSize
}
</script>
```

### Custom Upload Area

```vue
<template>
  <van-uploader>
    <van-button icon="plus" type="primary">Upload Image</van-button>
  </van-uploader>
</template>
```

### Preview Cover

```vue
<template>
  <van-uploader v-model="fileList">
    <template #preview-cover="{ file }">
      <div class="preview-cover van-ellipsis">{{ file.name }}</div>
    </template>
  </van-uploader>
</template>

<script setup>
import { ref } from 'vue'

const fileList = ref([
  { url: 'https://fastly.jsdelivr.net/npm/@vant/assets/leaf.jpeg', name: 'Leaf' }
])
</script>

<style scoped>
.preview-cover {
  position: absolute;
  bottom: 0;
  box-sizing: border-box;
  width: 100%;
  padding: 4px;
  color: #fff;
  font-size: 12px;
  text-align: center;
  background: rgba(0, 0, 0, 0.3);
}
</style>
```

### Preview Size

```vue
<template>
  <van-uploader v-model="fileList" preview-size="60" />
</template>

<script setup>
import { ref } from 'vue'

const fileList = ref([
  { url: 'https://fastly.jsdelivr.net/npm/@vant/assets/leaf.jpeg' }
])
</script>
```

### Before Read

```vue
<template>
  <van-uploader :before-read="beforeRead" />
</template>

<script setup>
import { showToast } from 'vant'

const beforeRead = (file) => {
  if (file.type !== 'image/jpeg') {
    showToast('Please upload an image in jpg format')
    return false
  }
  return true
}

const asyncBeforeRead = (file) => {
  return new Promise((resolve, reject) => {
    if (file.type !== 'image/jpeg') {
      showToast('Please upload an image in jpg format')
      reject()
    } else {
      const img = new File(['foo'], 'bar.jpg', { type: 'image/jpeg' })
      resolve(img)
    }
  })
}
</script>
```

### Disable Uploader

```vue
<template>
  <van-uploader disabled />
</template>
```

### Enable Reupload

```vue
<template>
  <van-uploader v-model="fileList" reupload max-count="2" />
</template>

<script setup>
import { ref } from 'vue'

const fileList = ref([
  { url: 'https://fastly.jsdelivr.net/npm/@vant/assets/leaf.jpeg' }
])
</script>
```

### Complete Upload Example

```vue
<template>
  <div class="upload-page">
    <van-uploader
      v-model="fileList"
      multiple
      :max-count="5"
      :max-size="5 * 1024 * 1024"
      :after-read="afterRead"
      :before-delete="beforeDelete"
      @oversize="onOversize"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { showToast, showConfirmDialog } from 'vant'

const fileList = ref([])

const afterRead = async (file) => {
  file.status = 'uploading'
  file.message = 'Uploading...'

  try {
    await uploadFile(file.file)
    file.status = 'done'
    file.message = 'Success'
    showToast('Upload successful')
  } catch (error) {
    file.status = 'failed'
    file.message = 'Failed'
    showToast('Upload failed')
  }
}

const uploadFile = (file) => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve({ url: 'https://example.com/image.jpg' })
    }, 2000)
  })
}

const beforeDelete = async (file) => {
  try {
    await showConfirmDialog({
      title: 'Delete',
      message: 'Are you sure to delete this file?'
    })
    return true
  } catch {
    return false
  }
}

const onOversize = () => {
  showToast('File size cannot exceed 5MB')
}
</script>
```

### Avatar Upload

```vue
<template>
  <div class="avatar-upload">
    <van-uploader
      v-model="avatar"
      :max-count="1"
      :after-read="afterRead"
      preview-size="100"
    >
      <template #default>
        <div class="upload-avatar">
          <van-icon name="user-o" size="40" />
          <span>Upload Avatar</span>
        </div>
      </template>
    </van-uploader>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const avatar = ref([])

const afterRead = async (file) => {
  file.status = 'uploading'
  file.message = 'Uploading...'
  
  await new Promise(resolve => setTimeout(resolve, 1500))
  
  file.status = 'done'
  showToast('Avatar uploaded')
}
</script>

<style scoped>
.avatar-upload {
  display: flex;
  justify-content: center;
  padding: 32px;
}

.upload-avatar {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100px;
  height: 100px;
  background: #f7f8fa;
  border-radius: 50%;
  color: #969799;
}

.upload-avatar span {
  margin-top: 8px;
  font-size: 12px;
}
</style>
```

### With Form

```vue
<template>
  <van-form @submit="onSubmit">
    <van-field name="uploader" label="Images">
      <template #input>
        <van-uploader v-model="fileList" multiple :max-count="3" />
      </template>
    </van-field>
    <div style="margin: 16px;">
      <van-button round block type="primary" native-type="submit">
        Submit
      </van-button>
    </div>
  </van-form>
</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'

const fileList = ref([])

const onSubmit = () => {
  showToast(`Submitted ${fileList.value.length} files`)
}
</script>
```

## Best Practices

1. **File Validation**: Use before-read for file type and size validation
2. **Upload Feedback**: Show upload status and progress
3. **Error Handling**: Handle upload failures gracefully
4. **Size Limits**: Set reasonable file size limits
5. **Count Limits**: Limit number of files for better UX
6. **Preview**: Enable preview for better user experience
7. **Accessibility**: Provide clear upload instructions
8. **Mobile Optimization**: Use capture attribute for camera access
