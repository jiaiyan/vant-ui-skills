---
name: "van-config-provider"
description: "Global configuration component for Vant. Invoke when user needs to enable dark mode, customize themes, override CSS variables, or configure global component settings."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant ConfigProvider Component

Global configuration component for Vant with dark mode, theme customization, and CSS variable override capabilities.

## When to Invoke

Invoke this skill when:
- User needs to enable dark mode globally
- User wants to customize theme colors
- User needs to override CSS variables
- User wants to configure global component settings
- User asks about theme switching
- User needs to set global z-index for popup components
- User wants to customize icon prefix globally

## Features

- **Dark Mode**: Enable dark theme globally
- **Theme Switching**: Dynamic theme switching between light and dark
- **CSS Variables**: Override CSS variables for customization
- **Theme Scopes**: Local or global CSS variable scope
- **Dark/Light Specific Variables**: Define variables for specific themes
- **Z-Index Configuration**: Set global z-index for popup components
- **Icon Prefix**: Customize global icon className prefix
- **TypeScript Support**: Full TypeScript type definitions

## API Reference

### Props

| Name | Description | Type | Default |
|------|-------------|------|---------|
| theme | Theme mode, can be set to `dark` | `ConfigProviderTheme` | `light` |
| theme-vars | Theme variables | `object` | - |
| theme-vars-dark | Theme variables that work in dark mode, will override `theme-vars` | `object` | - |
| theme-vars-light | Theme variables that work in light mode, will override `theme-vars` | `object` | - |
| theme-vars-scope | CSS variables scope, set to `global` for entire page | `ConfigProviderThemeVarsScope` | `local` |
| z-index | Set the z-index of all popup components globally | `number` | `2000` |
| tag | HTML tag of root element | `string` | `div` |
| icon-prefix | Icon className prefix | `string` | `van-icon` |

### Types

```ts
import type {
  ConfigProviderProps,
  ConfigProviderTheme,
  ConfigProviderThemeVars,
  ConfigProviderThemeVarsScope,
} from 'vant';
```

## Usage Examples

### Enable Dark Mode

```vue
<template>
  <van-config-provider theme="dark">
    <van-form>
      <van-field name="username" label="Username" />
      <van-field name="password" label="Password" />
      <div style="margin: 16px">
        <van-button round block type="primary">Submit</van-button>
      </div>
    </van-form>
  </van-config-provider>
</template>
```

### Switch Theme Dynamically

```vue
<template>
  <div>
    <van-button @click="toggleTheme">
      Switch to {{ theme === 'light' ? 'Dark' : 'Light' }}
    </van-button>
    
    <van-config-provider :theme="theme">
      <van-cell-group>
        <van-cell title="Cell title" value="Content" />
        <van-cell title="Cell title" value="Content" />
      </van-cell-group>
    </van-config-provider>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const theme = ref('light')

const toggleTheme = () => {
  theme.value = theme.value === 'light' ? 'dark' : 'light'
}
</script>
```

### Custom Theme Variables

```vue
<template>
  <van-config-provider :theme-vars="themeVars">
    <van-form>
      <van-field name="rate" label="Rate">
        <template #input>
          <van-rate v-model="rate" />
        </template>
      </van-field>
      <van-field name="slider" label="Slider">
        <template #input>
          <van-slider v-model="slider" />
        </template>
      </van-field>
      <div style="margin: 16px">
        <van-button round block type="primary" native-type="submit">
          Submit
        </van-button>
      </div>
    </van-form>
  </van-config-provider>
</template>

<script setup>
import { ref, reactive } from 'vue'

const rate = ref(4)
const slider = ref(50)

const themeVars = reactive({
  rateIconFullColor: '#07c160',
  sliderBarHeight: '4px',
  sliderButtonWidth: '20px',
  sliderButtonHeight: '20px',
  sliderActiveBackground: '#07c160',
  buttonPrimaryBackground: '#07c160',
  buttonPrimaryBorderColor: '#07c160',
})
</script>
```

### Global CSS Variables Scope

```vue
<template>
  <van-config-provider :theme-vars="themeVars" theme-vars-scope="global">
    <van-button type="primary">Global Theme</van-button>
  </van-config-provider>
</template>

<script setup>
import { reactive } from 'vue'

const themeVars = reactive({
  primaryColor: '#07c160',
  buttonPrimaryBackground: '#07c160',
})
</script>
```

### Theme-Specific Variables

```vue
<template>
  <van-config-provider
    :theme="theme"
    :theme-vars="themeVars"
    :theme-vars-dark="themeVarsDark"
    :theme-vars-light="themeVarsLight"
  >
    <van-button type="primary">Primary Button</van-button>
  </van-config-provider>
</template>

<script setup>
import { ref, reactive } from 'vue'

const theme = ref('light')

const themeVars = reactive({
  buttonPrimaryBackground: 'red'
})

const themeVarsDark = reactive({
  buttonPrimaryBackground: 'blue'
})

const themeVarsLight = reactive({
  buttonPrimaryBackground: 'green'
})
</script>
```

### Override Basic Variables

```vue
<template>
  <van-config-provider
    :theme-vars="themeVars"
    theme-vars-scope="global"
  >
    <van-button type="primary">Primary</van-button>
    <van-button type="success">Success</van-button>
    <van-button type="danger">Danger</van-button>
  </van-config-provider>
</template>

<script setup>
import { reactive } from 'vue'

const themeVars = reactive({
  primaryColor: '#1989fa',
  successColor: '#07c160',
  dangerColor: '#ee0a24',
})
</script>
```

### Set Global Z-Index

```vue
<template>
  <van-config-provider :z-index="3000">
    <van-button @click="showPopup = true">Show Popup</van-button>
    <van-popup v-model:show="showPopup">Popup content</van-popup>
  </van-config-provider>
</template>

<script setup>
import { ref } from 'vue'

const showPopup = ref(false)
</script>
```

### Custom Icon Prefix

```vue
<template>
  <van-config-provider icon-prefix="my-icon">
    <van-icon name="extra" />
    <van-button icon="extra" type="primary">Custom Icon</van-button>
  </van-config-provider>
</template>

<style>
@font-face {
  font-family: 'my-icon';
  src: url('./my-icon.ttf') format('truetype');
}

.my-icon {
  font-family: 'my-icon';
}

.my-icon-extra::before {
  content: '\e626';
}
</style>
```

### Complete Theme Configuration

```vue
<template>
  <van-config-provider
    :theme="theme"
    :theme-vars="themeVars"
    :theme-vars-dark="themeVarsDark"
    theme-vars-scope="global"
    :z-index="3000"
  >
    <div class="app">
      <van-nav-bar title="App" />
      
      <van-cell-group>
        <van-cell title="Theme" :value="theme" is-link @click="toggleTheme" />
        <van-cell title="Primary Color">
          <van-button type="primary" size="small">Primary</van-button>
        </van-cell>
      </van-cell-group>
      
      <van-tabbar v-model="active">
        <van-tabbar-item icon="home-o">Home</van-tabbar-item>
        <van-tabbar-item icon="search">Search</van-tabbar-item>
        <van-tabbar-item icon="user-o">Profile</van-tabbar-item>
      </van-tabbar>
    </div>
  </van-config-provider>
</template>

<script setup>
import { ref, reactive } from 'vue'

const theme = ref('light')
const active = ref(0)

const themeVars = reactive({
  primaryColor: '#1989fa',
  navBarBackgroundColor: '#fff',
  tabbarBackgroundColor: '#fff',
})

const themeVarsDark = reactive({
  primaryColor: '#3a7afe',
  navBarBackgroundColor: '#1a1a1a',
  tabbarBackgroundColor: '#1a1a1a',
})

const toggleTheme = () => {
  theme.value = theme.value === 'light' ? 'dark' : 'light'
}
</script>
```

## Basic Variables List

Vant provides the following basic CSS variables that can be customized:

### Color Palette

```css
--van-black: #000;
--van-white: #fff;
--van-gray-1: #f7f8fa;
--van-gray-2: #f2f3f5;
--van-gray-3: #ebedf0;
--van-gray-4: #dcdee0;
--van-gray-5: #c8c9cc;
--van-gray-6: #969799;
--van-gray-7: #646566;
--van-gray-8: #323233;
--van-red: #ee0a24;
--van-blue: #1989fa;
--van-orange: #ff976a;
--van-orange-dark: #ed6a0c;
--van-orange-light: #fffbe8;
--van-green: #07c160;
```

### Gradient Colors

```css
--van-gradient-red: linear-gradient(to right, #ff6034, #ee0a24);
--van-gradient-orange: linear-gradient(to right, #ffd01e, #ff8917);
```

### Component Colors

```css
--van-primary-color: var(--van-blue);
--van-success-color: var(--van-green);
--van-danger-color: var(--van-red);
--van-warning-color: var(--van-orange);
--van-text-color: var(--van-gray-8);
--van-text-color-2: var(--van-gray-6);
--van-text-color-3: var(--van-gray-5);
--van-active-color: var(--van-gray-2);
--van-active-opacity: 0.6;
--van-disabled-opacity: 0.5;
--van-background: var(--van-gray-1);
--van-background-2: var(--van-white);
```

### Padding

```css
--van-padding-base: 4px;
--van-padding-xs: 8px;
--van-padding-sm: 12px;
--van-padding-md: 16px;
--van-padding-lg: 24px;
--van-padding-xl: 32px;
```

### Font

```css
--van-font-size-xs: 10px;
--van-font-size-sm: 12px;
--van-font-size-md: 14px;
--van-font-size-lg: 16px;
--van-font-bold: 600;
--van-line-height-xs: 14px;
--van-line-height-sm: 18px;
--van-line-height-md: 20px;
--van-line-height-lg: 22px;
```

### Border

```css
--van-border-color: var(--van-gray-3);
--van-border-width: 1px;
--van-radius-sm: 2px;
--van-radius-md: 4px;
--van-radius-lg: 8px;
--van-radius-max: 999px;
```

## Common Issues

### 1. CSS Variables Not Taking Effect

Make sure to use `theme-vars-scope="global"` for basic variables:

```vue
<van-config-provider
  :theme-vars="{ primaryColor: 'red' }"
  theme-vars-scope="global"
>
  <!-- Components here -->
</van-config-provider>
```

### 2. Dark Mode Background Not Changed

Dark mode doesn't automatically change page background. Set it manually:

```css
.van-theme-dark body {
  color: #f5f5f5;
  background-color: black;
}
```

### 3. Variable Naming Convention

Convert camelCase to kebab-case for CSS variables:

```js
const themeVars = {
  buttonPrimaryBackground: '#07c160', // converts to --van-button-primary-background
}
```

## Best Practices

1. **Use global scope for basic variables**: Basic variables should use `theme-vars-scope="global"`
2. **Separate dark/light variables**: Use `theme-vars-dark` and `theme-vars-light` for theme-specific styles
3. **TypeScript support**: Use `ConfigProviderThemeVars` type for better intellisense
4. **Wrap at root level**: Place ConfigProvider at the root of your app for global configuration
5. **Test both themes**: Always test your app in both light and dark modes
6. **Document custom variables**: Keep track of customized variables for maintenance
7. **Use CSS class names**: You can also use `.van-theme-light` and `.van-theme-dark` class names for styling
