---
name: "vant-quickstart"
description: "Helps set up and configure Vant in Vue 3 projects. Invoke when user needs to install, import, or configure Vant in a new or existing project."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Quick Start

This skill provides comprehensive guidance for setting up Vant in Vue 3 projects, including installation, import methods, and framework integration.

## When to Invoke

Invoke this skill when:
- User wants to install Vant in a Vue 3 project
- User needs help with basic usage vs on-demand import
- User asks about configuring Vant with Vite, Rsbuild, Webpack, or Nuxt
- User encounters issues with Vant installation or setup
- User wants to create a new project with Vant

## Installation Methods

### Package Manager Installation

```bash
# npm - install latest Vant for Vue 3 project
npm i vant

# npm - install Vant 2 for Vue 2 project
npm i vant@latest-v2

# yarn
yarn add vant

# pnpm
pnpm add vant

# Bun
bun add vant
```

### CDN Import

For simple HTML pages, you can directly include CDN links:

```html
<!-- import style -->
<link rel="stylesheet" href="https://fastly.jsdelivr.net/npm/vant@4/lib/index.css" />

<!-- import script -->
<script src="https://fastly.jsdelivr.net/npm/vue@3"></script>
<script src="https://fastly.jsdelivr.net/npm/vant@4/lib/vant.min.js"></script>

<script>
  const app = Vue.createApp({
    template: `<van-button>Button</van-button>`,
  });
  app.use(vant);
  app.use(vant.Lazyload);
  vant.showToast('Message');
  app.mount('#app');
</script>
```

**Free CDN Options:**
- [jsdelivr](https://www.jsdelivr.com/package/npm/vant)
- [cdnjs](https://cdnjs.com/libraries/vant)
- [unpkg](https://unpkg.com/)

> Note: Free CDN is generally used for making prototypes or personal projects. It is not recommended to use free CDN in production environment.

## Usage Methods

### Basic Usage

Vant supports Tree Shaking by default:

```js
import { createApp } from 'vue';
import { Button } from 'vant';
import 'vant/lib/index.css';

const app = createApp();
app.use(Button);
```

> Tip: Vant supports Tree Shaking by default, so you don't need to configure any plugins. The unused JS code will be removed by Tree Shaking, but CSS styles cannot be optimized by it.

### On-Demand Import (Recommended for CSS Optimization)

Install required plugins:

```bash
npm i @vant/auto-import-resolver unplugin-vue-components unplugin-auto-import -D
```

#### Vite Configuration

```js
import vue from '@vitejs/plugin-vue';
import AutoImport from 'unplugin-auto-import/vite';
import Components from 'unplugin-vue-components/vite';
import { VantResolver } from '@vant/auto-import-resolver';

export default {
  plugins: [
    vue(),
    AutoImport({
      resolvers: [VantResolver()],
    }),
    Components({
      resolvers: [VantResolver()],
    }),
  ],
};
```

#### Rsbuild Configuration

```js
import { defineConfig } from '@rsbuild/core';
import { pluginVue } from '@rsbuild/plugin-vue';
import AutoImport from 'unplugin-auto-import/rspack';
import Components from 'unplugin-vue-components/rspack';
import { VantResolver } from '@vant/auto-import-resolver';

export default defineConfig({
  plugins: [pluginVue()],
  tools: {
    rspack: {
      plugins: [
        AutoImport({
          resolvers: [VantResolver()],
        }),
        Components({
          resolvers: [VantResolver()],
        }),
      ],
    },
  },
});
```

#### Webpack / Vue CLI Configuration

```js
const { VantResolver } = require('@vant/auto-import-resolver');
const AutoImport = require('unplugin-auto-import/webpack');
const Components = require('unplugin-vue-components/webpack');

module.exports = {
  configureWebpack: {
    plugins: [
      AutoImport({ resolvers: [VantResolver()] }),
      Components({ resolvers: [VantResolver()] }),
    ],
  },
};
```

### Using Components After Configuration

```html
<template>
  <van-button type="primary" />
</template>

<script>
  showToast('No need to import showToast');
</script>
```

## Framework Integration

### Nuxt 3 Integration

Install the Nuxt module:

```bash
npm i @vant/nuxt -D
```

Add to Nuxt config:

```js
export default defineNuxtConfig({
  modules: ['@vant/nuxt'],
});
```

Then use components directly:

```html
<template>
  <van-button type="primary" @click="showToast('toast')">button</van-button>
  <VanButton type="success" @click="showNotify('notify')">button</VanButton>
  <LazyVanButton type="default">lazy button</LazyVanButton>
</template>
```

## Creating New Projects

### Using Rsbuild (Recommended)

Rsbuild is a build tool based on Rspack, developed by the author of Vant:

```bash
npm create rsbuild@latest
```

### Example Projects

- [vant-demo - rsbuild](https://github.com/vant-ui/vant-demo/tree/master/vant/rsbuild): Vue 3, Vant 4, and Rsbuild
- [vant-demo - vite](https://github.com/vant-ui/vant-demo/tree/master/vant/vite): Vue 3, Vant 4, and Vite
- [vant-demo - nuxt3](https://github.com/vant-ui/vant-demo/tree/master/vant/nuxt3): Vue 3, Nuxt 3, and Vant 4

## Important Tips

1. **"Full Import" and "On-demand Import" should not be used at the same time**, otherwise it will lead to problems such as code duplication and style overrides.

2. **For unplugin-vue-components >= 0.26.0**, use `ComponentsPlugin.default` for webpack, vue-cli, and rspack.

3. If the component cannot be imported, report issues to [unplugin-vue-components](https://github.com/antfu/unplugin/unplugin-vue-components).

4. If styles don't work, report issues to the Vant repository.

## Input Parameters

When using this skill, provide the following information:
- **Project type**: Vite, Rsbuild, Webpack, Vue CLI, Nuxt, or CDN
- **Import method**: Basic usage or on-demand import
- **Vue version**: Vue 3 (default) or Vue 2
- **Package manager**: npm, yarn, pnpm, or bun

## Output Format

This skill provides:
1. Installation commands for the specified package manager
2. Configuration code snippets for the build tool
3. Component usage examples
4. Troubleshooting tips for common setup issues

## Usage Limitations

- Vant 4 requires Vue 3.x
- Vant 2 is available for Vue 2 projects
- CDN usage is not recommended for production applications
- For SSR projects, additional configuration may be needed
