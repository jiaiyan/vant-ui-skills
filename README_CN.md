# Vant UI Skills Library

一个全面的 Vant UI 移动端组件库技能库，专为 AI 智能体理解和运用 Vant 组件而设计。

**[English Version](./README.md)**

***

## 📖 简介

Vant UI 是一个轻量、可靠的移动端组件库，于 2017 年开源，目前是 Vue 移动端组件库中 Star 数量最高的项目。

本技能库为全部 Vant 技能提供结构化文档和使用指南，包括：

- **86 个组件技能** - 单个组件文档及 API 参考
- **11 个 Composable 技能** - Vue 3 Composition API 工具函数
- **6 个基础技能** - 快速开始、主题定制、国际化、组件总览、Composables 总览、高级用法

## ✨ 功能特性

- **完整的 API 文档** - 包含属性、事件、方法和插槽
- **使用示例** - 基础和进阶用法模式
- **最佳实践** - 推荐的实现指南
- **移动端优化** - 针对移动端场景的最佳实践
- **Vue 3 Composition API** - 完整的 Composables 支持
- **跨平台兼容** - 适用于任何智能体环境

## 📁 目录结构

```
vant-skills/
├── components/                    # 86 个组件技能
│   ├── van-button/
│   ├── van-cell/
│   ├── van-form/
│   ├── van-list/
│   ├── van-popup/
│   ├── van-swipe/
│   └── ...
├── composables/                   # 11 个 组合式 API 技能
│   ├── use-click-away/
│   ├── use-count-down/
│   ├── use-rect/
│   ├── use-window-size/
│   └── ...
├── vant-components/               # 组件总览索引
├── vant-composables/              # 组合式 API 总览索引
├── vant-quickstart/               # 快速开始指南
├── vant-theming/                  # 主题定制
├── vant-i18n/                     # 国际化
├── vant-advanced-usage/           # 进阶用法
├── AGENTS.md                      # 智能体文档
├── SKILL.md                       # 主技能入口
├── README.md                      # 英文说明
└── README_CN.md                   # 中文说明
```

## 🚀 安装

### 前置条件

- Node.js 16+
- Vue 3.2+
- Vant 4.0+

### 安装步骤

```bash
# 安装 Vant
npm install vant

# 或使用 yarn
yarn add vant

# 或使用 pnpm
pnpm add vant
```

### 安装 Vant UI Skills 技能库

将 Vant UI Skills 技能库添加到您的项目中，以便 AI 智能体能够理解和使用 Vant 组件：

```bash
npx skills add https://github.com/jiaiyan/vant-ui-skills --skill vant-ui-skills
```

## 📚 使用方法

### 适用于 AI 智能体

每个技能文件遵循统一的格式：

```yaml
---
name: "van-button"
description: "按钮组件描述..."
metadata:
  author: jiaiyan
  version: "1.0.0"
---
```

### 技能分类

| 分类          | 数量 | 描述                                                                                                                                                                                 |
| ----------- | -- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 基础组件        | 10 | Button、Cell、Icon、Image、Popup、Toast、ConfigProvider、Space、Style、Col/Row                                                                                                              |
| 表单组件        | 19 | Form、Field、Calendar、Cascader、Checkbox、DatePicker、NumberKeyboard、PasswordInput、Picker、PickerGroup、Radio、Rate、Search、Signature、Slider、Stepper、Switch、TimePicker、Uploader             |
| 交互组件        | 12 | ActionSheet、Barrage、Dialog、DropdownMenu、FloatingBubble、FloatingPanel、Loading、Notify、Overlay、PullRefresh、ShareSheet、SwipeCell                                                       |
| 展示组件        | 26 | Badge、Circle、Collapse、CountDown、Divider、Empty、Highlight、ImagePreview、Lazyload、List、NoticeBar、Popover、Progress、RollingText、Skeleton、Steps、Sticky、Swipe、Tag、TextEllipsis、Watermark 等 |
| 导航组件        | 10 | ActionBar、BackTop、Grid、IndexBar、NavBar、Pagination、Sidebar、Tab、Tabbar、TreeSelect                                                                                                    |
| 业务组件        | 9  | AddressEdit、AddressList、Area、Card、ContactCard、ContactEdit、ContactList、CouponList、SubmitBar                                                                                         |
| Composables | 11 | useClickAway、useCountDown、useCustomFieldValue、useEventListener、usePageVisibility、useRaf、useRect、useRelation、useScrollParent、useToggle、useWindowSize                                |
| 基础技能        | 6  | vant-quickstart、vant-theming、vant-i18n、vant-advanced-usage、vant-components、vant-composables                                                                                        |

### 快速引用

```markdown
# 访问组件技能
./components/van-{name}/SKILL.md

# 访问 Composable 技能
./composables/use-{name}/SKILL.md

# 访问基础技能
./vant-{name}/SKILL.md
```

## 🔧 组件示例

### 基础用法

```vue
<template>
  <van-button type="primary">主要按钮</van-button>
  <van-field v-model="value" placeholder="请输入内容" />
  <van-cell-group>
    <van-cell title="单元格" value="内容" />
    <van-cell title="单元格" value="内容" is-link />
  </van-cell-group>
</template>
```

### 带验证的表单

```vue
<template>
  <van-form @submit="onSubmit">
    <van-field
      v-model="username"
      name="用户名"
      label="用户名"
      placeholder="用户名"
      :rules="[{ required: true, message: '请填写用户名' }]"
    />
    <van-field
      v-model="password"
      type="password"
      name="密码"
      label="密码"
      placeholder="密码"
      :rules="[{ required: true, message: '请填写密码' }]"
    />
    <div style="margin: 16px;">
      <van-button round block type="primary" native-type="submit">
        提交
      </van-button>
    </div>
  </van-form>
</template>
```

### 列表加载

```vue
<template>
  <van-list
    v-model:loading="loading"
    :finished="finished"
    finished-text="没有更多了"
    @load="onLoad"
  >
    <van-cell
      v-for="item in list"
      :key="item"
      :title="item"
    />
  </van-list>
</template>

<script setup>
import { ref } from 'vue';

const list = ref([]);
const loading = ref(false);
const finished = ref(false);

const onLoad = () => {
  setTimeout(() => {
    for (let i = 0; i < 10; i++) {
      list.value.push(list.value.length + 1);
    }
    loading.value = false;
    if (list.value.length >= 40) {
      finished.value = true;
    }
  }, 1000);
};
</script>
```

### Composable 使用示例

```vue
<template>
  <div>
    <p>窗口尺寸: {{ width }} x {{ height }}</p>
    <button @click="toggle()">{{ show ? '隐藏' : '显示' }}</button>
  </div>
</template>

<script setup>
import { useWindowSize, useToggle } from '@vant/use';

const { width, height } = useWindowSize();
const [show, toggle] = useToggle();
</script>
```

## 📊 技能统计

| 类别                    | 数量      |
| --------------------- | ------- |
| Basic Components      | 10      |
| Form Components       | 19      |
| Action Components     | 12      |
| Display Components    | 26      |
| Navigation Components | 10      |
| Business Components   | 9       |
| Composables           | 11      |
| Foundation            | 6       |
| **总计**                | **103** |

## 🤝 贡献指南

欢迎参与贡献！请遵循以下步骤：

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/new-skill`)
3. 提交更改 (`git commit -m 'Add new skill'`)
4. 推送到分支 (`git push origin feature/new-skill`)
5. 创建 Pull Request

### 技能文件规范

每个技能文件应包含：

- **name**: 唯一标识符（如 `van-button`）
- **description**: 清晰的描述及调用条件
- **metadata**: 作者和版本信息
- **内容章节**:
  - 使用场景 (When to Invoke)
  - 基础用法 (Basic Usage)
  - API 参考 (API Reference)
  - 常见模式 (Common Patterns)
  - 最佳实践 (Best Practices)

## 📋 技能文件模板

```markdown
---
name: "van-{component-name}"
description: "组件描述。当用户需要...时调用"
metadata:
  author: your-name
  version: "1.0.0"
---

# 组件名称

组件描述和概述。

## When to Invoke

- 场景 1
- 场景 2

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
| prop | 描述 | type | default |

### Events

| Name | Description | Parameters |
|------|-------------|------------|
| event | 描述 | params |

### Slots

| Name | Description |
|------|-------------|
| slot | 描述 |

## Best Practices

1. 实践 1
2. 实践 2
```

## 📄 许可证

MIT License

Copyright (c) 2024 Vant UI Skills Library

特此免费授予任何获得本软件副本和相关文档文件（"软件"）的人不受限制地处置该软件的权利，包括不受限制地使用、复制、修改、合并、发布、分发、再授权和/或出售该软件副本，以及再授权以配备了上述权利的人员使用该软件。

上述版权声明和本许可声明应包含在该软件的所有副本或实质性成分中。

本软件按"原样"提供，不提供任何形式的担保，包括但不限于适销性、特定用途适用性和非侵权性担保。在任何情况下，作者或版权持有人均不对任何索赔、损害或其他责任负责，无论这些追责基于合同、侵权或其他行为，还是产生于、源于或有关于本软件以及本软件的使用或其他处置。

## 🔗 相关资源

- [Vant 官方文档](https://vant-ui.github.io/vant/#/zh-CN)
- [Vue 3 官方文档](https://cn.vuejs.org/)
- [Vant GitHub](https://github.com/youzan/vant)
- [Vant 示例项目](https://github.com/youzan/vant-demo)

## 📞 支持

如有问题和需要支持：

- 在 GitHub 上提交 Issue
- 查阅官方文档
- 加入 Vant 社区

