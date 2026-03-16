# Vant UI Skills Library

A comprehensive skill library for Vant UI framework, designed for AI agents to understand and utilize Vant mobile components effectively.

**[中文版本](./README_CN.md)**

***

## 📖 Introduction

Vant UI is a lightweight, reliable mobile component library. This skill library provides structured documentation and usage guidelines for Vant components, including:

- **86 Component Skills** - Individual component documentation with API reference
- **11 Composable Skills** - Vue 3 Composition API utilities
- **6 Foundation Skills** - Quickstart, Theming, i18n, Components Overview, Composables Overview, Advanced Usage

Vant is specifically designed for mobile web applications, offering excellent performance and user experience on mobile devices.

## ✨ Features

- **Complete API Documentation** - Props, events, slots, and methods for each component
- **Mobile-First Design** - Optimized for mobile web applications
- **Usage Examples** - Basic and advanced usage patterns
- **Best Practices** - Recommended implementation guidelines for mobile scenarios
- **Vue 3 Composition API** - Full Composables support
- **Cross-Platform Compatibility** - Works in any agent environment
- **Lightweight** - Minimal bundle size with tree-shaking support

## 📁 Directory Structure

```
vant-skills/
├── components/                    # 86 Component Skills
│   ├── van-button/
│   ├── van-cell/
│   ├── van-field/
│   ├── van-form/
│   ├── van-nav-bar/
│   ├── van-tabbar/
│   ├── van-toast/
│   ├── van-dialog/
│   └── ...
├── composables/                   # 11 Composable API Skills
│   ├── use-click-away/
│   ├── use-count-down/
│   ├── use-rect/
│   ├── use-window-size/
│   └── ...
├── vant-components/               # Component Overview Index
├── vant-composables/              # Composables API Overview Index
├── vant-quickstart/               # Quick Start Guide
├── vant-theming/                  # Theme Customization
├── vant-i18n/                     # Internationalization
├── vant-advanced-usage/           # Advanced Usage
├── AGENTS.md                      # Agents Documentation
├── SKILL.md                       # Main Skill Entry
├── README.md                      # English README
└── README_CN.md                   # Chinese README
```

## 🚀 Installation

### Prerequisites

- Node.js 16+
- Vue 3.2+
- Vant 4.0+

### Setup

```bash
# Install Vant
npm install vant

# Install icons (optional)
npm install @vant/icons
```

### Install Vant UI Skills Library

Add the Vant UI Skills library to your project, enabling AI agents to understand and utilize Vant components:

```bash
npx skills add https://github.com/jiaiyan/vant-ui-skills --skill vant-ui-skills
```

## 📚 Usage

### For AI Agents

Each skill file follows a consistent format:

```yaml
---
name: "van-button"
description: "Button component description..."
metadata:
  author: jiaiyan
  version: "1.0.0"
---
```

### Skill Categories

| Category              | Count | Description                                                                                                                                                                                                |
| --------------------- | ----- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Basic Components      | 10    | Button, Cell, Icon, Image, Popup, Toast, ConfigProvider, Space, Style, Col/Row                                                                                                                             |
| Form Components       | 19    | Form, Field, Calendar, Cascader, Checkbox, DatePicker, NumberKeyboard, PasswordInput, Picker, PickerGroup, Radio, Rate, Search, Signature, Slider, Stepper, Switch, TimePicker, Uploader                   |
| Action Components     | 12    | ActionSheet, Barrage, Dialog, DropdownMenu, FloatingBubble, FloatingPanel, Loading, Notify, Overlay, PullRefresh, ShareSheet, SwipeCell                                                                    |
| Display Components    | 26    | Badge, Circle, Collapse, CountDown, Divider, Empty, Highlight, ImagePreview, Lazyload, List, NoticeBar, Popover, Progress, RollingText, Skeleton, Steps, Sticky, Swipe, Tag, TextEllipsis, Watermark, etc. |
| Navigation Components | 10    | ActionBar, BackTop, Grid, IndexBar, NavBar, Pagination, Sidebar, Tab, Tabbar, TreeSelect                                                                                                                   |
| Business Components   | 9     | AddressEdit, AddressList, Area, Card, ContactCard, ContactEdit, ContactList, CouponList, SubmitBar                                                                                                         |
| Composables           | 11    | useClickAway, useCountDown, useCustomFieldValue, useEventListener, usePageVisibility, useRaf, useRect, useRelation, useScrollParent, useToggle, useWindowSize                                              |
| Foundation Skills     | 6     | vant-quickstart, vant-theming, vant-i18n, vant-advanced-usage, vant-components, vant-composables                                                                                                           |

### Quick Reference

```markdown
# Access component skill
./components/van-{name}/SKILL.md

# Access composable skill
./composables/use-{name}/SKILL.md

# Access foundation skill
./vant-{name}/SKILL.md
```

## 🔧 Component Examples

### Basic Usage

```vue
<template>
  <van-button type="primary">Primary Button</van-button>
  <van-field v-model="value" placeholder="Please input" />
  <van-cell-group>
    <van-cell title="Cell" value="Content" />
  </van-cell-group>
</template>
```

### Form with Validation

```vue
<template>
  <van-form @submit="onSubmit">
    <van-field
      v-model="username"
      name="username"
      label="Username"
      placeholder="Username"
      :rules="[{ required: true, message: 'Please input username' }]"
    />
    <van-field
      v-model="password"
      type="password"
      name="password"
      label="Password"
      placeholder="Password"
      :rules="[{ required: true, message: 'Please input password' }]"
    />
    <div style="margin: 16px;">
      <van-button round block type="primary" native-type="submit">
        Submit
      </van-button>
    </div>
  </van-form>
</template>

<script setup>
import { ref } from 'vue';

const username = ref('');
const password = ref('');

const onSubmit = (values) => {
  console.log('submit', values);
};
</script>
```

### Navigation Bar

```vue
<template>
  <van-nav-bar
    title="Title"
    left-text="Back"
    left-arrow
    @click-left="onClickLeft"
  />
</template>

<script setup>
import { showToast } from 'vant';

const onClickLeft = () => {
  showToast('Back');
};
</script>
```

### Toast and Dialog

```vue
<template>
  <van-button @click="showToast">Show Toast</van-button>
  <van-button @click="showDialog">Show Dialog</van-button>
</template>

<script setup>
import { showToast, showDialog } from 'vant';

const showToast = () => {
  showToast('This is a toast message');
};

const showDialog = () => {
  showDialog({
    title: 'Title',
    message: 'This is a dialog message',
  });
};
</script>
```

### Composable Usage

```vue
<template>
  <div>
    <p>Window size: {{ width }} x {{ height }}</p>
    <button @click="toggle()">{{ show ? 'Hide' : 'Show' }}</button>
  </div>
</template>

<script setup>
import { useWindowSize, useToggle } from '@vant/use';

const { width, height } = useWindowSize();
const [show, toggle] = useToggle();
</script>
```

## 📊 Skills Statistics

| Category              | Count   |
| --------------------- | ------- |
| Basic Components      | 10      |
| Form Components       | 19      |
| Action Components     | 12      |
| Display Components    | 26      |
| Navigation Components | 10      |
| Business Components   | 9       |
| Composables           | 11      |
| Foundation            | 6       |
| **Total**             | **103** |

## 🤝 Contributing

We welcome contributions! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-skill`)
3. Commit your changes (`git commit -m 'Add new skill'`)
4. Push to the branch (`git push origin feature/new-skill`)
5. Open a Pull Request

### Skill File Guidelines

Each skill file should include:

- **name**: Unique identifier (e.g., `van-button`)
- **description**: Clear description with invocation criteria
- **metadata**: Author and version information
- **Content Sections**:
  - When to Invoke
  - Basic Usage
  - API Reference
  - Common Patterns
  - Best Practices

## 📋 Skill File Template

```markdown
---
name: "van-{component-name}"
description: "Component description. Invoke when user needs to..."
metadata:
  author: your-name
  version: "1.0.0"
---

# Component Name

Component description and overview.

## When to Invoke

- Use case 1
- Use case 2

## Basic Usage

\`\`\`vue
<template>
  <van-component />
</template>
\`\`\`

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| prop | Description | type | default |

### Events

| Name | Description | Parameters |
|------|-------------|------------|
| event | Description | params |

### Slots

| Name | Description |
|------|-------------|
| slot | Description |

## Best Practices

1. Practice 1
2. Practice 2
```

## 📄 License

MIT License

Copyright (c) 2024 Vant UI Skills Library

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

## 🔗 Related Resources

- [Vant Documentation](https://vant-ui.github.io/vant/)
- [Vue 3 Documentation](https://vuejs.org/)
- [Vant GitHub](https://github.com/youzan/vant)
- [Vant Demo](https://vant-ui.github.io/vant/#/home)

## 📞 Support

For questions and support:

- Open an issue on GitHub
- Check the documentation
- Join the Vant community

