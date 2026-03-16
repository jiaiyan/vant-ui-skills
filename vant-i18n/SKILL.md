---
name: "vant-i18n"
description: "Helps configure internationalization in Vant projects. Invoke when user needs to switch languages, add custom translations, or support multiple locales."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Internationalization

This skill provides comprehensive guidance for configuring internationalization (i18n) in Vant projects, including language switching, custom translations, and multi-language support.

## When to Invoke

Invoke this skill when:
- User wants to switch Vant to a different language
- User needs to customize default translations
- User asks about supported languages
- User wants to add a new language pack
- User needs to get the current language setting

## Basic Usage

### Switch Languages

Vant uses Chinese as the default language. Use `Locale.use` method to switch languages:

```js
import { Locale } from 'vant';
import enUS from 'vant/es/locale/lang/en-US';

Locale.use('en-US', enUS);
```

### Override Default Configs

Use `Locale.add` method to modify default translations:

```js
import { Locale } from 'vant';

const messages = {
  'en-US': {
    vanPicker: {
      confirm: 'Close',
    },
  },
};

Locale.add(messages);
```

### Get Current Language

Use `useCurrentLang` method to get the current language:

```ts
import { useCurrentLang } from 'vant';

const currentLang = useCurrentLang();

console.log(currentLang.value); // --> 'en-US'
```

## Supported Languages

| Language | Filename | Version |
|----------|----------|---------|
| Arabic | ar-SA | v3.5.0 |
| Bulgarian | bg-BG | v3.5.0 |
| Bangla (Bangladesh) | bn-BD | v3.4.5 |
| Chinese | zh-CN | - |
| Traditional Chinese (HK) | zh-HK | - |
| Traditional Chinese (TW) | zh-TW | - |
| Danish | da-DK | v3.4.8 |
| German | de-DE | - |
| German (formal) | de-DE-formal | - |
| Greek | el-GR | v3.5.0 |
| English | en-US | - |
| Esperanto | eo-EO | v4.0.9 |
| Spanish (Spain) | es-ES | - |
| Farsi | fa-IR | v3.5.0 |
| French | fr-FR | - |
| Hebrew | he-IL | v3.5.0 |
| Hindi | hi-IN | v3.4.3 |
| Indonesian | id-ID | v3.4.5 |
| Icelandic | is-IS | v3.4.7 |
| Italian | it-IT | v3.4.5 |
| Japanese | ja-JP | - |
| Kazakh | kk-KZ | - |
| Khmer | km-KH | v4.1.2 |
| Korean | ko-KR | v3.4.3 |
| Lao | la-LA | v3.4.7 |
| Mongolian | mm-MN | v4.0.5 |
| Norwegian | nb-NO | - |
| Dutch | nl-NL | v4.0.5 |
| Polish | pl-PL | v4.9.17 |
| Portuguese (Brazil) | pt-BR | v3.3.3 |
| Romanian | ro-RO | - |
| Russian | ru-RU | v3.1.5 |
| Serbian | sr-RS | v4.6.4 |
| Swedish | sv-SE | v3.4.7 |
| Thai | th-TH | - |
| Turkish | tr-TR | - |
| Ukrainian | uk-UA | v3.4.5 |
| Vietnamese | vi-VN | v3.4.5 |

> View all language configs [Here](https://github.com/vant-ui/vant/tree/main/packages/vant/src/locale/lang).

## Common Component Translations

### Picker Component

```js
import { Locale } from 'vant';

Locale.add({
  'en-US': {
    vanPicker: {
      confirm: 'Confirm',
      cancel: 'Cancel',
    },
  },
});
```

### Dialog Component

```js
import { Locale } from 'vant';

Locale.add({
  'en-US': {
    vanDialog: {
      confirm: 'OK',
      cancel: 'Cancel',
    },
  },
});
```

### Calendar Component

```js
import { Locale } from 'vant';

Locale.add({
  'en-US': {
    vanCalendar: {
      confirm: 'Confirm',
      title: 'Select Date',
      weekdays: ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'],
      monthTitle: (year: number, month: number) => `${year}/${month}`,
      rangePrompt: (maxRange: number) => `Choose no more than ${maxRange} days`,
    },
  },
});
```

## Integration with Vue I18n

### Setup with Vue I18n

```js
import { createApp } from 'vue';
import { createI18n } from 'vue-i18n';
import { Locale } from 'vant';
import enUS from 'vant/es/locale/lang/en-US';
import zhCN from 'vant/es/locale/lang/zh-CN';

const i18n = createI18n({
  locale: 'en-US',
  messages: {
    'en-US': { message: 'hello' },
    'zh-CN': { message: '你好' },
  },
});

const app = createApp();
app.use(i18n);

Locale.use('en-US', enUS);
```

### Sync Language Switching

```js
import { Locale } from 'vant';
import { useI18n } from 'vue-i18n';
import enUS from 'vant/es/locale/lang/en-US';
import zhCN from 'vant/es/locale/lang/zh-CN';

const { locale } = useI18n();

const langMap = {
  'en-US': enUS,
  'zh-CN': zhCN,
};

function switchLanguage(lang) {
  locale.value = lang;
  Locale.use(lang, langMap[lang]);
}
```

## Adding New Languages

If you can't find the language you need, you can:

1. **Submit a Pull Request** to add the new language pack
2. Refer to [Add German language pack](https://github.com/vant-ui/vant/pull/7245) PR for guidance

### Custom Language Pack Structure

```js
export default {
  name: 'Language Name',
  vanPicker: {
    confirm: 'Confirm',
    cancel: 'Cancel',
  },
  vanDialog: {
    confirm: 'OK',
    cancel: 'Cancel',
  },
  vanCalendar: {
    confirm: 'Confirm',
    title: 'Select Date',
    weekdays: ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'],
    monthTitle: (year, month) => `${year}/${month}`,
  },
  vanContactCard: {
    addText: 'Add Contact',
  },
  vanPullRefresh: {
    pulling: 'Pull to refresh...',
    loosing: 'Loose to refresh...',
    loading: 'Loading...',
  },
};
```

## Best Practices

1. **Initialize early**: Set the language before creating the Vue app instance.

2. **Sync with app locale**: Keep Vant locale in sync with your app's i18n locale.

3. **Lazy load language packs**: For better performance, load language packs on demand:

```js
async function switchLanguage(lang) {
  const messages = await import(`vant/es/locale/lang/${lang}`);
  Locale.use(lang, messages.default);
}
```

4. **Customize component texts**: Override specific component texts without changing the entire language pack.

5. **Handle RTL languages**: For RTL languages like Arabic, add appropriate CSS:

```css
[lang="ar-SA"] {
  direction: rtl;
}
```

## Input Parameters

When using this skill, provide the following information:
- **Target language**: The language code to switch to
- **Custom translations**: Any component texts to override
- **Integration needs**: Whether using Vue I18n or other i18n library
- **Dynamic switching**: Whether runtime language switching is needed

## Output Format

This skill provides:
1. Language switching code examples
2. Custom translation configuration
3. Vue I18n integration guide
4. Lazy loading implementation
5. Best practices for multi-language support

## Usage Limitations

- Language packs are bundled separately and need to be imported explicitly
- Some language packs may be incomplete and require additional translations
- RTL language support requires additional CSS configuration
