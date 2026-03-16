# Vant UI Skills - Agents Documentation

This document provides detailed information about all agents (skills) available in the Vant UI Skills Library.

## 📋 Agent Index

| Category                                               | Skills Count | Description                         |
| ------------------------------------------------------ | ------------ | ----------------------------------- |
| [Basic Components](#basic-components-agents)           | 10           | UI elements for basic interactions  |
| [Form Components](#form-components-agents)             | 19           | Form inputs and data collection     |
| [Action Components](#action-components-agents)         | 12           | User action and feedback components |
| [Display Components](#display-components-agents)       | 26           | Data visualization and presentation |
| [Navigation Components](#navigation-components-agents) | 10           | Navigation and routing components   |
| [Business Components](#business-components-agents)     | 9            | Business-specific components        |
| [Composables](#composables-agents)                     | 11           | Vue 3 composition API utilities     |
| [Foundation](#foundation-agents)                       | 6            | Core setup and configuration        |

***

## Basic Components Agents

### van-button

**Description**: Basic button with various types, sizes, and styles for user interactions.

**Use Cases**:

- Form submissions
- Action triggers
- Navigation controls
- Interactive elements

**Parameters**:

| Parameter     | Type    | Default   | Description                                      |
| ------------- | ------- | --------- | ------------------------------------------------ |
| type          | string  | 'default' | Type: primary, success, warning, danger, default |
| size          | string  | 'normal'  | Size: large, normal, small, mini                 |
| plain         | boolean | false     | Plain style                                      |
| round         | boolean | false     | Round corners                                    |
| square        | boolean | false     | Square shape                                     |
| disabled      | boolean | false     | Disabled state                                   |
| loading       | boolean | false     | Loading state                                    |
| icon          | string  | -         | Icon name                                        |
| icon-position | string  | 'left'    | Icon position: left, right                       |
| block         | boolean | false     | Full width button                                |

**Example**:

```vue
<van-button type="primary" @click="handleClick">Primary Button</van-button>
<van-button type="success" plain>Plain Success</van-button>
<van-button loading type="primary">Loading...</van-button>
```

***

### van-cell

**Description**: Displays a list item with title, value, and optional icon.

**Use Cases**:

- Settings lists
- Menu items
- Information display
- Navigation links

**Parameters**:

| Parameter       | Type          | Default    | Description                            |
| --------------- | ------------- | ---------- | -------------------------------------- |
| title           | string/number | -          | Left title                             |
| value           | string/number | -          | Right value                            |
| label           | string        | -          | Description below title                |
| icon            | string        | -          | Left icon name                         |
| icon-prefix     | string        | 'van-icon' | Icon class prefix                      |
| is-link         | boolean       | false      | Show link arrow                        |
| required        | boolean       | false      | Show required asterisk                 |
| clickable       | boolean       | false      | Enable click feedback                  |
| title-style     | object/string | -          | Title style                            |
| title-class     | string        | -          | Title class                            |
| value-class     | string        | -          | Value class                            |
| label-class     | string        | -          | Label class                            |
| arrow-direction | string        | 'right'    | Arrow direction: left, up, down, right |

**Example**:

```vue
<van-cell-group>
  <van-cell title="Cell Title" value="Content" />
  <van-cell title="With Icon" icon="location-o" is-link />
  <van-cell title="Clickable" is-link @click="handleClick" />
</van-cell-group>
```

***

### van-config-provider

**Description**: Global configuration wrapper for Vant components.

**Use Cases**:

- Global theme configuration
- Internationalization
- Component size settings

**Parameters**:

| Parameter   | Type   | Default    | Description            |
| ----------- | ------ | ---------- | ---------------------- |
| theme       | string | 'light'    | Theme: light, dark     |
| theme-vars  | object | -          | CSS variable overrides |
| icon-prefix | string | 'van-icon' | Global icon prefix     |
| tag         | string | 'div'      | Root element tag       |

**Example**:

```vue
<van-config-provider :theme-vars="themeVars">
  <van-button type="primary">Themed Button</van-button>
</van-config-provider>

<script setup>
const themeVars = {
  buttonPrimaryBackgroundColor: '#07c160',
  buttonPrimaryBorderColor: '#07c160'
};
</script>
```

***

### van-icon

**Description**: SVG icons with customizable size and color.

**Use Cases**:

- UI icons
- Button icons
- Status indicators
- Navigation icons

**Parameters**:

| Parameter    | Type          | Default    | Description          |
| ------------ | ------------- | ---------- | -------------------- |
| name         | string        | -          | Icon name (required) |
| dot          | boolean       | false      | Show red dot         |
| badge        | string/number | -          | Badge content        |
| color        | string        | -          | Icon color           |
| size         | string/number | 'inherit'  | Icon size            |
| class-prefix | string        | 'van-icon' | Class prefix         |

**Example**:

```vue
<van-icon name="chat-o" size="20" />
<van-icon name="success" color="#07c160" />
<van-icon name="cart-o" badge="5" />
```

***

### van-image

**Description**: Image component with lazy load and error handling.

**Use Cases**:

- Image display
- Lazy loading images
- Image placeholders
- Responsive images

**Parameters**:

| Parameter    | Type          | Default      | Description                                        |
| ------------ | ------------- | ------------ | -------------------------------------------------- |
| src          | string        | -            | Image URL                                          |
| fit          | string        | 'fill'       | Object-fit: contain, cover, fill, none, scale-down |
| position     | string        | 'center'     | Object-position                                    |
| alt          | string        | -            | Alt text                                           |
| width        | string/number | -            | Width                                              |
| height       | string/number | -            | Height                                             |
| radius       | string/number | -            | Border radius                                      |
| round        | boolean       | false        | Round shape                                        |
| lazy-load    | boolean       | false        | Enable lazy load                                   |
| show-error   | boolean       | true         | Show error placeholder                             |
| show-loading | boolean       | true         | Show loading placeholder                           |
| error-icon   | string        | 'photo-fail' | Error icon                                         |
| loading-icon | string        | 'photo'      | Loading icon                                       |

**Example**:

```vue
<van-image
  width="100"
  height="100"
  fit="cover"
  src="https://example.com/image.jpg"
/>
<van-image lazy-load src="image.jpg" />
```

***

### van-col / van-row

**Description**: 24-column grid system for layout.

**Use Cases**:

- Responsive layouts
- Grid systems
- Column-based designs

**Parameters (van-row)**:

| Parameter | Type          | Default | Description                                                           |
| --------- | ------------- | ------- | --------------------------------------------------------------------- |
| gutter    | string/number | -       | Column gap                                                            |
| justify   | string        | 'start' | Horizontal alignment: start, center, end, space-around, space-between |
| align     | string        | 'top'   | Vertical alignment: top, center, bottom                               |
| wrap      | boolean       | true    | Allow wrapping                                                        |

**Parameters (van-col)**:

| Parameter | Type          | Default | Description        |
| --------- | ------------- | ------- | ------------------ |
| span      | string/number | -       | Column span (1-24) |
| offset    | string/number | -       | Column offset      |
| tag       | string        | 'div'   | Element tag        |

**Example**:

```vue
<van-row gutter="20">
  <van-col span="8">span: 8</van-col>
  <van-col span="8">span: 8</van-col>
  <van-col span="8">span: 8</van-col>
</van-row>

<van-row justify="center">
  <van-col span="6">col</van-col>
  <van-col span="6">col</van-col>
</van-row>
```

***

### van-popup

**Description**: Popup layer component for overlays and modals.

**Use Cases**:

- Modal dialogs
- Bottom sheets
- Side panels
- Overlay content

**Parameters**:

| Parameter              | Type          | Default     | Description                                |
| ---------------------- | ------------- | ----------- | ------------------------------------------ |
| v-model:show           | boolean       | false       | Show popup                                 |
| position               | string        | 'center'    | Position: top, bottom, right, left, center |
| overlay                | boolean       | true        | Show overlay                               |
| overlay-class          | string        | -           | Overlay class                              |
| overlay-style          | object        | -           | Overlay style                              |
| close-on-click-overlay | boolean       | true        | Close on overlay click                     |
| lock-scroll            | boolean       | true        | Lock body scroll                           |
| round                  | boolean       | false       | Round corners                              |
| closeable              | boolean       | false       | Show close icon                            |
| close-icon             | string        | 'cross'     | Close icon name                            |
| close-icon-position    | string        | 'top-right' | Close icon position                        |
| safe-area-inset-bottom | boolean       | false       | Enable safe area                           |
| teleport               | string        | 'body'      | Teleport target                            |
| duration               | string/number | 0.3         | Animation duration                         |

**Example**:

```vue
<van-popup v-model:show="show" position="bottom" round>
  <div class="content">Popup Content</div>
</van-popup>

<van-popup v-model:show="show" position="left" :style="{ width: '80%', height: '100%' }">
  Side Panel
</van-popup>
```

***

### van-space

**Description**: Consistent spacing between elements.

**Use Cases**:

- Element spacing
- Button groups
- Form layouts
- Inline arrangements

**Parameters**:

| Parameter | Type                | Default      | Description                                              |
| --------- | ------------------- | ------------ | -------------------------------------------------------- |
| direction | string              | 'horizontal' | Direction: horizontal, vertical                          |
| size      | string/number/array | 'small'      | Spacing size or \[h, v]                                  |
| align     | string              | -            | Alignment: start, center, end, baseline                  |
| justify   | string              | -            | Justify: start, center, end, space-around, space-between |
| wrap      | boolean             | true         | Allow wrapping                                           |
| fill      | boolean             | false        | Fill container                                           |

**Example**:

```vue
<van-space>
  <van-button type="primary">Button 1</van-button>
  <van-button type="primary">Button 2</van-button>
</van-space>

<van-space direction="vertical" fill>
  <van-button block>Button 1</van-button>
  <van-button block>Button 2</van-button>
</van-space>
```

***

### van-style

**Description**: Inline CSS style injection component.

**Use Cases**:

- Dynamic CSS injection
- Scoped styles
- Runtime style updates

**Example**:

```vue
<van-style>
  .custom-class {
    color: red;
  }
</van-style>
```

***

### van-toast

**Description**: Lightweight toast notification for feedback.

**Use Cases**:

- Operation feedback
- Loading indicators
- Success/error messages
- Quick notifications

**Parameters**:

| Parameter      | Type          | Default    | Description                              |
| -------------- | ------------- | ---------- | ---------------------------------------- |
| type           | string        | 'text'     | Type: text, loading, success, fail, html |
| message        | string        | -          | Message content                          |
| duration       | number        | 2000       | Display duration (ms), 0 for persistent  |
| position       | string        | 'middle'   | Position: top, middle, bottom            |
| icon           | string        | -          | Custom icon                              |
| icon-size      | string/number | -          | Icon size                                |
| forbid-click   | boolean       | false      | Forbid background click                  |
| close-on-click | boolean       | false      | Close on click                           |
| overlay        | boolean       | false      | Show overlay                             |
| loading-type   | string        | 'circular' | Loading type: circular, spinner          |

**Example**:

```js
import { showToast, showLoadingToast, showSuccessToast } from 'vant';

showToast('Message');
showLoadingToast({ message: 'Loading...', forbidClick: true });
showSuccessToast('Success!');
```

***

## Form Components Agents

### van-calendar

**Description**: Calendar component for date selection.

**Use Cases**:

- Date selection
- Date range selection
- Booking systems
- Schedule management

**Parameters**:

| Parameter             | Type          | Default   | Description                   |
| --------------------- | ------------- | --------- | ----------------------------- |
| v-model:show          | boolean       | false     | Show calendar                 |
| type                  | string        | 'single'  | Type: single, range, multiple |
| title                 | string        | -         | Calendar title                |
| color                 | string        | '#1989fa' | Theme color                   |
| min-date              | Date          | -         | Minimum date                  |
| max-date              | Date          | -         | Maximum date                  |
| default-date          | Date/Array    | -         | Default selected date         |
| row-height            | string/number | 64        | Row height                    |
| formatter             | function      | -         | Day formatter                 |
| poppable              | boolean       | true      | Show as popup                 |
| show-mark             | boolean       | true      | Show month mark               |
| show-title            | boolean       | true      | Show title                    |
| show-subtitle         | boolean       | true      | Show subtitle                 |
| show-confirm          | boolean       | true      | Show confirm button           |
| confirm-text          | string        | -         | Confirm button text           |
| confirm-disabled-text | string        | -         | Disabled confirm text         |
| first-day-of-week     | number        | 0         | First day of week (0-6)       |

**Example**:

```vue
<van-calendar v-model:show="show" @confirm="onConfirm" />

<van-calendar
  v-model:show="show"
  type="range"
  :min-date="minDate"
  :max-date="maxDate"
  @confirm="onRangeConfirm"
/>
```

***

### van-cascader

**Description**: Cascader selection for hierarchical data.

**Use Cases**:

- Region selection
- Category hierarchies
- Multi-level data selection

**Parameters**:

| Parameter    | Type         | Default         | Description        |
| ------------ | ------------ | --------------- | ------------------ |
| v-model      | string/array | -               | Selected value     |
| title        | string       | -               | Popup title        |
| options      | array        | \[]             | Options data       |
| placeholder  | string       | 'Please Select' | Placeholder        |
| active-color | string       | '#1989fa'       | Active color       |
| closeable    | boolean      | true            | Show close icon    |
| show-header  | boolean      | true            | Show header        |
| close-icon   | string       | 'cross'         | Close icon         |
| field-names  | object       | -               | Custom field names |

**Example**:

```vue
<van-cascader
  v-model="value"
  title="Select Region"
  :options="options"
  @finish="onFinish"
/>

<script setup>
const options = [
  {
    text: 'Zhejiang',
    value: '330000',
    children: [{ text: 'Hangzhou', value: '330100' }]
  }
];
</script>
```

***

### van-checkbox

**Description**: Checkbox for multiple selections.

**Use Cases**:

- Multiple selections
- Check-all functionality
- Toggle states
- Agreement checkboxes

**Parameters**:

| Parameter      | Type          | Default   | Description                 |
| -------------- | ------------- | --------- | --------------------------- |
| v-model        | boolean/array | -         | Checked state               |
| name           | string/number | -         | Checkbox name               |
| shape          | string        | 'round'   | Shape: round, square        |
| disabled       | boolean       | false     | Disabled state              |
| label-disabled | boolean       | false     | Disable label click         |
| label-position | string        | 'right'   | Label position: left, right |
| icon-size      | string/number | '20px'    | Icon size                   |
| checked-color  | string        | '#1989fa' | Checked color               |
| bind-group     | boolean       | true      | Bind to group               |
| indeterminate  | boolean       | false     | Indeterminate state         |

**Example**:

```vue
<van-checkbox v-model="checked">Checkbox</van-checkbox>

<van-checkbox-group v-model="result" direction="horizontal">
  <van-checkbox name="a">A</van-checkbox>
  <van-checkbox name="b">B</van-checkbox>
  <van-checkbox name="c">C</van-checkbox>
</van-checkbox-group>
```

***

### van-date-picker

**Description**: Date picker for selecting dates.

**Use Cases**:

- Date input
- Date range selection
- Birthday selection
- Schedule selection

**Parameters**:

| Parameter          | Type          | Default                   | Description      |
| ------------------ | ------------- | ------------------------- | ---------------- |
| v-model            | Date          | -                         | Selected date    |
| columns-type       | array         | \['year', 'month', 'day'] | Column types     |
| min-date           | Date          | -                         | Minimum date     |
| max-date           | Date          | -                         | Maximum date     |
| title              | string        | -                         | Picker title     |
| loading            | boolean       | false                     | Loading state    |
| readonly           | boolean       | false                     | Readonly state   |
| item-height        | string/number | 44                        | Item height      |
| visible-item-count | number        | 6                         | Visible items    |
| swipe-duration     | string/number | 1000                      | Swipe duration   |
| filter             | function      | -                         | Column filter    |
| formatter          | function      | -                         | Column formatter |

**Example**:

```vue
<van-date-picker
  v-model="selectedDate"
  title="Select Date"
  :min-date="minDate"
  :max-date="maxDate"
  @confirm="onConfirm"
  @cancel="onCancel"
/>
```

***

### van-field

**Description**: Input field for forms with various types.

**Use Cases**:

- Text input
- Password input
- Textarea
- Form fields

**Parameters**:

| Parameter           | Type           | Default | Description                                                     |
| ------------------- | -------------- | ------- | --------------------------------------------------------------- |
| v-model             | string/number  | -       | Input value                                                     |
| label               | string         | -       | Field label                                                     |
| name                | string         | -       | Field name                                                      |
| type                | string         | 'text'  | Input type: text, number, digit, tel, email, password, textarea |
| size                | string         | -       | Size: large                                                     |
| maxlength           | string/number  | -       | Maximum length                                                  |
| placeholder         | string         | -       | Placeholder                                                     |
| border              | boolean        | true    | Show border                                                     |
| disabled            | boolean        | false   | Disabled state                                                  |
| readonly            | boolean        | false   | Readonly state                                                  |
| required            | boolean        | false   | Show required mark                                              |
| clearable           | boolean        | false   | Show clear button                                               |
| clear-trigger       | string         | 'focus' | Clear trigger: always, focus                                    |
| clickable           | boolean        | false   | Enable click feedback                                           |
| is-link             | boolean        | false   | Show link arrow                                                 |
| autofocus           | boolean        | false   | Auto focus                                                      |
| show-word-limit     | boolean        | false   | Show word limit                                                 |
| error               | boolean        | false   | Error state                                                     |
| error-message       | string         | -       | Error message                                                   |
| error-message-align | string         | 'left'  | Error message align                                             |
| autocomplete        | string         | -       | Autocomplete attribute                                          |
| label-align         | string         | 'left'  | Label alignment                                                 |
| label-width         | string/number  | -       | Label width                                                     |
| input-align         | string         | 'left'  | Input alignment                                                 |
| autosize            | boolean/object | false   | Auto resize textarea                                            |
| left-icon           | string         | -       | Left icon                                                       |
| right-icon          | string         | -       | Right icon                                                      |
| rules               | array          | -       | Validation rules                                                |

**Example**:

```vue
<van-field v-model="value" label="Username" placeholder="Enter username" />

<van-field
  v-model="password"
  type="password"
  label="Password"
  placeholder="Enter password"
  :rules="[{ required: true, message: 'Required' }]"
/>

<van-field
  v-model="message"
  rows="2"
  autosize
  label="Message"
  type="textarea"
  maxlength="50"
  placeholder="Enter message"
  show-word-limit
/>
```

***

### van-form

**Description**: Form management with validation support.

**Use Cases**:

- Data collection
- Form validation
- Form submission
- Complex form layouts

**Parameters**:

| Parameter           | Type          | Default  | Description                         |
| ------------------- | ------------- | -------- | ----------------------------------- |
| label-width         | string/number | '6.2em'  | Label width                         |
| label-align         | string        | 'left'   | Label alignment                     |
| input-align         | string        | 'left'   | Input alignment                     |
| error-message-align | string        | 'left'   | Error message alignment             |
| validate-trigger    | string        | 'onBlur' | Validation trigger                  |
| colon               | boolean       | false    | Show colon after label              |
| required            | string        | -        | Required mark style: asterisk, auto |
| show-error          | boolean       | false    | Show error in field                 |
| show-error-message  | boolean       | true     | Show error message                  |
| submit-on-enter     | boolean       | true     | Submit on enter                     |

**Example**:

```vue
<van-form @submit="onSubmit">
  <van-field
    v-model="username"
    name="username"
    label="Username"
    placeholder="Username"
    :rules="[{ required: true, message: 'Required' }]"
  />
  <van-field
    v-model="password"
    type="password"
    name="password"
    label="Password"
    placeholder="Password"
    :rules="[{ required: true, message: 'Required' }]"
  />
  <div style="margin: 16px;">
    <van-button round block type="primary" native-type="submit">Submit</van-button>
  </div>
</van-form>
```

***

### van-number-keyboard

**Description**: Virtual numeric keyboard for secure input.

**Use Cases**:

- PIN entry
- Secure number input
- Touch-friendly number input
- Payment amount input

**Parameters**:

| Parameter              | Type          | Default   | Description            |
| ---------------------- | ------------- | --------- | ---------------------- |
| v-model                | string        | -         | Input value            |
| show                   | boolean       | false     | Show keyboard          |
| title                  | string        | -         | Keyboard title         |
| theme                  | string        | 'default' | Theme: default, custom |
| maxlength              | string/number | -         | Maximum length         |
| transition             | boolean       | true      | Transition animation   |
| z-index                | string/number | 100       | z-index                |
| extra-key              | string/array  | -         | Extra key(s)           |
| close-button-text      | string        | -         | Close button text      |
| delete-button-text     | string        | -         | Delete button text     |
| close-button-loading   | boolean       | false     | Close button loading   |
| hide-on-click-outside  | boolean       | true      | Hide on outside click  |
| safe-area-inset-bottom | boolean       | true      | Enable safe area       |
| random-key-order       | boolean       | false     | Randomize key order    |

**Example**:

```vue
<van-field v-model="value" readonly clickable @click="show = true" />
<van-number-keyboard
  v-model="value"
  :show="show"
  :maxlength="6"
  @blur="show = false"
/>
```

***

### van-password-input

**Description**: Password input with masked display.

**Use Cases**:

- PIN entry
- Password verification
- Secure code input
- OTP input

**Parameters**:

| Parameter  | Type          | Default | Description       |
| ---------- | ------------- | ------- | ----------------- |
| value      | string        | -       | Password value    |
| length     | string/number | 6       | Password length   |
| gutter     | string/number | 0       | Gap between items |
| mask       | boolean       | true    | Show mask         |
| focused    | boolean       | false   | Focus state       |
| error-info | string        | -       | Error message     |
| info       | string        | -       | Info message      |

**Example**:

```vue
<van-password-input
  :value="password"
  :focused="showKeyboard"
  @focus="showKeyboard = true"
/>
<van-number-keyboard
  v-model="password"
  :show="showKeyboard"
  @blur="showKeyboard = false"
/>
```

***

### van-picker

**Description**: Picker component for selecting values from lists.

**Use Cases**:

- Single selection
- Multi-column selection
- Date/time selection
- Custom option selection

**Parameters**:

| Parameter           | Type          | Default | Description                   |
| ------------------- | ------------- | ------- | ----------------------------- |
| v-model             | string/array  | -       | Selected value(s)             |
| columns             | array         | \[]     | Column data                   |
| title               | string        | -       | Picker title                  |
| loading             | boolean       | false   | Loading state                 |
| readonly            | boolean       | false   | Readonly state                |
| item-height         | string/number | 44      | Item height                   |
| visible-item-count  | number        | 6       | Visible items                 |
| swipe-duration      | string/number | 1000    | Swipe duration                |
| columns-field-names | object        | -       | Custom field names            |
| toolbar-position    | string        | 'top'   | Toolbar position: top, bottom |
| show-toolbar        | boolean       | true    | Show toolbar                  |
| allow-html          | boolean       | false   | Allow HTML in options         |
| option-filter       | function      | -       | Option filter                 |

**Example**:

```vue
<van-picker
  v-model="selectedValue"
  title="Select"
  :columns="columns"
  @confirm="onConfirm"
  @cancel="onCancel"
/>

<script setup>
const columns = [
  { text: 'Option 1', value: '1' },
  { text: 'Option 2', value: '2' },
  { text: 'Option 3', value: '3' }
];
</script>
```

***

### van-picker-group

**Description**: Group multiple pickers together.

**Use Cases**:

- Multi-picker combinations
- Date-time selection
- Complex selection scenarios

**Parameters**:

| Parameter           | Type   | Default | Description         |
| ------------------- | ------ | ------- | ------------------- |
| v-model             | array  | -       | Selected values     |
| title               | string | -       | Group title         |
| tabs                | array  | \[]     | Tab labels          |
| next-step-text      | string | -       | Next button text    |
| confirm-button-text | string | -       | Confirm button text |

**Example**:

```vue
<van-picker-group
  v-model="values"
  title="Select Date"
  :tabs="['Year', 'Month', 'Day']"
  @confirm="onConfirm"
>
  <van-picker :columns="yearColumns" />
  <van-picker :columns="monthColumns" />
  <van-picker :columns="dayColumns" />
</van-picker-group>
```

***

### van-radio

**Description**: Radio button for single selection.

**Use Cases**:

- Single selection
- Option groups
- Settings selection
- Choice selection

**Parameters**:

| Parameter      | Type                  | Default   | Description                 |
| -------------- | --------------------- | --------- | --------------------------- |
| v-model        | string/number/boolean | -         | Selected value              |
| name           | string/number         | -         | Radio name/value            |
| disabled       | boolean               | false     | Disabled state              |
| label-disabled | boolean               | false     | Disable label click         |
| label-position | string                | 'right'   | Label position: left, right |
| icon-size      | string/number         | '20px'    | Icon size                   |
| checked-color  | string                | '#1989fa' | Checked color               |
| shape          | string                | 'round'   | Shape: round, square        |

**Example**:

```vue
<van-radio-group v-model="checked" direction="horizontal">
  <van-radio name="1">Option A</van-radio>
  <van-radio name="2">Option B</van-radio>
  <van-radio name="3">Option C</van-radio>
</van-radio-group>
```

***

### van-rate

**Description**: Star rating component.

**Use Cases**:

- User ratings
- Product reviews
- Feedback scoring
- Quality assessment

**Parameters**:

| Parameter      | Type          | Default   | Description         |
| -------------- | ------------- | --------- | ------------------- |
| v-model        | number        | -         | Rating value        |
| count          | number        | 5         | Total stars         |
| size           | string/number | '20px'    | Star size           |
| gutter         | string/number | '4px'     | Star gap            |
| color          | string        | '#ffd21e' | Active star color   |
| void-color     | string        | '#c7c7c7' | Inactive star color |
| disabled-color | string        | '#c7c7c7' | Disabled star color |
| void-icon      | string        | 'star'    | Inactive star icon  |
| icon           | string        | 'star'    | Active star icon    |
| disabled       | boolean       | false     | Disabled state      |
| readonly       | boolean       | false     | Readonly state      |
| allow-half     | boolean       | false     | Allow half stars    |
| touchable      | boolean       | true      | Touch to rate       |

**Example**:

```vue
<van-rate v-model="rating" />
<van-rate v-model="rating" allow-half />
<van-rate v-model="rating" :count="10" size="15" />
```

***

### van-search

**Description**: Search input component.

**Use Cases**:

- Search functionality
- Filter inputs
- Quick search
- Auto-complete search

**Parameters**:

| Parameter     | Type          | Default   | Description          |
| ------------- | ------------- | --------- | -------------------- |
| v-model       | string        | -         | Search value         |
| label         | string        | -         | Left label           |
| shape         | string        | 'square'  | Shape: square, round |
| background    | string        | '#f2f2f2' | Background color     |
| maxlength     | string/number | -         | Maximum length       |
| placeholder   | string        | -         | Placeholder          |
| clearable     | boolean       | true      | Show clear button    |
| clear-trigger | string        | 'focus'   | Clear trigger        |
| autofocus     | boolean       | false     | Auto focus           |
| show-action   | boolean       | false     | Show action button   |
| action-text   | string        | 'Cancel'  | Action button text   |
| disabled      | boolean       | false     | Disabled state       |
| readonly      | boolean       | false     | Readonly state       |
| error         | boolean       | false     | Error state          |
| input-align   | string        | 'left'    | Input alignment      |
| left-icon     | string        | 'search'  | Left icon            |
| right-icon    | string        | -         | Right icon           |

**Example**:

```vue
<van-search v-model="value" placeholder="Search..." @search="onSearch" />

<van-search
  v-model="value"
  show-action
  placeholder="Search..."
  @search="onSearch"
  @cancel="onCancel"
/>
```

***

### van-slider

**Description**: Slider for selecting values within a range.

**Use Cases**:

- Volume controls
- Price range filters
- Progress indicators
- Range selections

**Parameters**:

| Parameter      | Type          | Default   | Description       |
| -------------- | ------------- | --------- | ----------------- |
| v-model        | number/array  | -         | Slider value      |
| max            | string/number | 100       | Maximum value     |
| min            | string/number | 0         | Minimum value     |
| step           | string/number | 1         | Step size         |
| bar-height     | string/number | '2px'     | Bar height        |
| button-size    | string/number | '24px'    | Button size       |
| active-color   | string        | '#1989fa' | Active color      |
| inactive-color | string        | '#e5e5e5' | Inactive color    |
| range          | boolean       | false     | Range mode        |
| reverse        | boolean       | false     | Reverse direction |
| disabled       | boolean       | false     | Disabled state    |
| readonly       | boolean       | false     | Readonly state    |
| vertical       | boolean       | false     | Vertical mode     |

**Example**:

```vue
<van-slider v-model="value" />
<van-slider v-model="value" range :min="-50" :max="50" />
<van-slider v-model="value" @change="onChange" />
```

***

### van-signature

**Description**: Signature pad for capturing signatures.

**Use Cases**:

- Digital signatures
- Drawing pads
- Handwriting capture
- Agreement signing

**Parameters**:

| Parameter           | Type   | Default   | Description         |
| ------------------- | ------ | --------- | ------------------- |
| pen-color           | string | '#000'    | Pen color           |
| line-width          | number | 3         | Line width          |
| background-color    | string | -         | Background color    |
| clear-button-text   | string | 'Clear'   | Clear button text   |
| confirm-button-text | string | 'Confirm' | Confirm button text |

**Example**:

```vue
<van-signature @submit="onSubmit" @clear="onClear" />
```

***

### van-stepper

**Description**: Numeric input with increment/decrement buttons.

**Use Cases**:

- Quantity inputs
- Numeric settings
- Counter controls
- Shopping cart quantity

**Parameters**:

| Parameter      | Type          | Default   | Description           |
| -------------- | ------------- | --------- | --------------------- |
| v-model        | number        | -         | Current value         |
| min            | string/number | 1         | Minimum value         |
| max            | string/number | -         | Maximum value         |
| default-value  | string/number | 1         | Default value         |
| step           | string/number | 1         | Step size             |
| name           | string/number | -         | Identifier            |
| input-width    | string/number | '32px'    | Input width           |
| button-size    | string/number | '28px'    | Button size           |
| decimal-length | string/number | -         | Decimal places        |
| theme          | string        | 'default' | Theme: default, round |
| placeholder    | string        | -         | Placeholder           |
| integer        | boolean       | false     | Integer only          |
| disabled       | boolean       | false     | Disabled state        |
| disable-plus   | boolean       | false     | Disable plus button   |
| disable-minus  | boolean       | false     | Disable minus button  |
| disable-input  | boolean       | false     | Disable input         |
| show-plus      | boolean       | true      | Show plus button      |
| show-minus     | boolean       | true      | Show minus button     |
| show-input     | boolean       | true      | Show input            |
| long-press     | boolean       | true      | Long press support    |
| allow-empty    | boolean       | false     | Allow empty value     |

**Example**:

```vue
<van-stepper v-model="value" />
<van-stepper v-model="value" min="1" max="10" />
<van-stepper v-model="value" theme="round" button-size="22" />
```

***

### van-switch

**Description**: Toggle switch for on/off states.

**Use Cases**:

- Enable/disable features
- Toggle settings
- On/off switches
- Boolean selections

**Parameters**:

| Parameter      | Type          | Default   | Description    |
| -------------- | ------------- | --------- | -------------- |
| v-model        | boolean       | -         | Switch state   |
| loading        | boolean       | false     | Loading state  |
| disabled       | boolean       | false     | Disabled state |
| size           | string/number | '26px'    | Switch size    |
| active-color   | string        | '#1989fa' | Active color   |
| inactive-color | string        | 'white'   | Inactive color |
| active-value   | any           | true      | Active value   |
| inactive-value | any           | false     | Inactive value |

**Example**:

```vue
<van-switch v-model="checked" />
<van-switch v-model="checked" loading />
<van-switch v-model="checked" size="24" active-color="#07c160" />
```

***

### van-time-picker

**Description**: Time picker for selecting time.

**Use Cases**:

- Time input
- Schedule selection
- Alarm setting
- Time range selection

**Parameters**:

| Parameter    | Type          | Default             | Description              |
| ------------ | ------------- | ------------------- | ------------------------ |
| v-model      | string        | -                   | Selected time (HH:mm:ss) |
| title        | string        | -                   | Picker title             |
| columns-type | array         | \['hour', 'minute'] | Column types             |
| min-hour     | string/number | 0                   | Minimum hour             |
| max-hour     | string/number | 23                  | Maximum hour             |
| min-minute   | string/number | 0                   | Minimum minute           |
| max-minute   | string/number | 59                  | Maximum minute           |
| min-second   | string/number | 0                   | Minimum second           |
| max-second   | string/number | 59                  | Maximum second           |
| filter       | function      | -                   | Column filter            |
| formatter    | function      | -                   | Column formatter         |

**Example**:

```vue
<van-time-picker v-model="time" title="Select Time" @confirm="onConfirm" />
```

***

### van-uploader

**Description**: File upload component with preview.

**Use Cases**:

- File uploads
- Image uploads
- Avatar uploads
- Document uploads

**Parameters**:

| Parameter          | Type          | Default      | Description                      |
| ------------------ | ------------- | ------------ | -------------------------------- |
| v-model            | array         | -            | File list                        |
| accept             | string        | 'image/\*'   | Accepted file types              |
| name               | string/number | -            | Upload name                      |
| preview-size       | string/number | '80px'       | Preview size                     |
| preview-full-image | boolean       | false        | Full image preview               |
| multiple           | boolean       | false        | Multiple files                   |
| disabled           | boolean       | false        | Disabled state                   |
| readonly           | boolean       | false        | Readonly state                   |
| deletable          | boolean       | true         | Show delete button               |
| show-upload        | boolean       | true         | Show upload button               |
| max-count          | string/number | -            | Maximum files                    |
| max-size           | string/number | -            | Maximum file size (bytes)        |
| result-type        | string        | 'dataUrl'    | Result type: dataUrl, text, file |
| upload-icon        | string        | 'photograph' | Upload icon                      |
| upload-text        | string        | -            | Upload text                      |
| after-read         | function      | -            | After read callback              |
| before-read        | function      | -            | Before read callback             |
| before-delete      | function      | -            | Before delete callback           |

**Example**:

```vue
<van-uploader v-model="fileList" multiple :max-count="3" />

<van-uploader
  v-model="fileList"
  :after-read="afterRead"
  :before-delete="beforeDelete"
/>
```

***

## Action Components Agents

### van-action-sheet

**Description**: Action sheet for selecting from a list of actions.

**Use Cases**:

- Action selection
- Share menus
- Option selection
- Confirmation actions

**Parameters**:

| Parameter              | Type    | Default     | Description            |
| ---------------------- | ------- | ----------- | ---------------------- |
| v-model:show           | boolean | false       | Show action sheet      |
| actions                | array   | \[]         | Action items           |
| title                  | string  | -           | Title                  |
| cancel-text            | string  | -           | Cancel button text     |
| description            | string  | -           | Description            |
| closeable              | boolean | false       | Show close icon        |
| close-icon             | string  | 'cross'     | Close icon             |
| close-icon-position    | string  | 'top-right' | Close icon position    |
| round                  | boolean | true        | Round corners          |
| overlay                | boolean | true        | Show overlay           |
| close-on-click-action  | boolean | true        | Close on action click  |
| close-on-click-overlay | boolean | true        | Close on overlay click |
| safe-area-inset-bottom | boolean | true        | Enable safe area       |

**Example**:

```vue
<van-action-sheet
  v-model:show="show"
  :actions="actions"
  @select="onSelect"
/>

<script setup>
const actions = [
  { name: 'Option 1', subname: 'Description' },
  { name: 'Option 2', disabled: true },
  { name: 'Option 3', loading: true }
];
</script>
```

***

### van-barrage

**Description**: Barrage/danmu component for displaying scrolling comments.

**Use Cases**:

- Live streaming comments
- Video danmu
- Scrolling messages
- Interactive overlays

**Parameters**:

| Parameter | Type    | Default | Description              |
| --------- | ------- | ------- | ------------------------ |
| v-model   | array   | -       | Barrage items            |
| auto-play | boolean | true    | Auto play                |
| duration  | number  | 4000    | Animation duration (ms)  |
| delay     | number  | 300     | Delay between items (ms) |
| top       | number  | 10      | Top offset               |
| rows      | number  | 4       | Number of rows           |

**Example**:

```vue
<van-barrage v-model="list">
  <template #item="{ item }">
    <span>{{ item.content }}</span>
  </template>
</van-barrage>
```

***

### van-dialog

**Description**: Modal dialog for alerts, confirms, and custom content.

**Use Cases**:

- Alert dialogs
- Confirmation dialogs
- Custom modal content
- Form dialogs

**Parameters**:

| Parameter              | Type          | Default   | Description                  |
| ---------------------- | ------------- | --------- | ---------------------------- |
| v-model:show           | boolean       | false     | Show dialog                  |
| title                  | string        | -         | Dialog title                 |
| width                  | string/number | '320px'   | Dialog width                 |
| message                | string        | -         | Message content              |
| message-align          | string        | 'center'  | Message alignment            |
| theme                  | string        | 'default' | Theme: default, round-button |
| show-confirm-button    | boolean       | true      | Show confirm button          |
| show-cancel-button     | boolean       | false     | Show cancel button           |
| confirm-button-text    | string        | -         | Confirm button text          |
| cancel-button-text     | string        | -         | Cancel button text           |
| confirm-button-color   | string        | -         | Confirm button color         |
| cancel-button-color    | string        | -         | Cancel button color          |
| overlay                | boolean       | true      | Show overlay                 |
| overlay-class          | string        | -         | Overlay class                |
| overlay-style          | object        | -         | Overlay style                |
| close-on-click-overlay | boolean       | false     | Close on overlay click       |
| close-on-popstate      | boolean       | false     | Close on popstate            |
| closeable              | boolean       | false     | Show close icon              |
| close-icon             | string        | 'cross'   | Close icon                   |
| round                  | boolean       | true      | Round corners                |
| teleport               | string        | 'body'    | Teleport target              |

**Example**:

```vue
<van-dialog v-model:show="show" title="Title" message="Content" />

<van-dialog v-model:show="show" title="Title" show-cancel-button>
  <van-field v-model="value" placeholder="Enter value" />
</van-dialog>

<script setup>
import { showDialog, showConfirmDialog } from 'vant';

showDialog({ message: 'Message' });
showConfirmDialog({ title: 'Confirm', message: 'Are you sure?' });
</script>
```

***

### van-dropdown-menu

**Description**: Dropdown menu for filtering and sorting.

**Use Cases**:

- Filter menus
- Sort options
- Category selection
- Multi-level filters

**Parameters**:

| Parameter              | Type          | Default   | Description            |
| ---------------------- | ------------- | --------- | ---------------------- |
| direction              | string        | 'down'    | Direction: up, down    |
| active-color           | string        | '#1989fa' | Active color           |
| close-on-click-outside | boolean       | true      | Close on outside click |
| close-on-click-overlay | boolean       | true      | Close on overlay click |
| duration               | string/number | 0.2       | Animation duration     |
| overlay                | boolean       | true      | Show overlay           |

**Example**:

```vue
<van-dropdown-menu>
  <van-dropdown-item v-model="value1" :options="option1" />
  <van-dropdown-item v-model="value2" :options="option2" />
</van-dropdown-menu>
```

***

### van-floating-bubble

**Description**: Draggable floating bubble component.

**Use Cases**:

- Quick actions
- Floating buttons
- Draggable elements
- Support buttons

**Parameters**:

| Parameter      | Type   | Default | Description          |
| -------------- | ------ | ------- | -------------------- |
| v-model:offset | object | -       | Position offset      |
| icon           | string | -       | Icon name            |
| axis           | string | 'y'     | Axis: x, y, xy, lock |
| magnetic       | string | -       | Magnetic: x, y, xy   |
| boundary       | object | -       | Boundary area        |

**Example**:

```vue
<van-floating-bubble icon="chat" @click="onClick" />
```

***

### van-floating-panel

**Description**: Draggable floating panel component.

**Use Cases**:

- Bottom sheets
- Draggable panels
- Expandable content
- Map overlays

**Parameters**:

| Parameter              | Type          | Default | Description        |
| ---------------------- | ------------- | ------- | ------------------ |
| v-model:height         | number        | 0       | Panel height       |
| anchors                | array         | -       | Anchor heights     |
| duration               | string/number | 0.3     | Animation duration |
| content-draggable      | boolean       | true    | Content draggable  |
| lock-scroll            | boolean       | false   | Lock scroll        |
| safe-area-inset-bottom | boolean       | false   | Enable safe area   |

**Example**:

```vue
<van-floating-panel v-model:height="height" :anchors="anchors">
  <div>Panel content</div>
</van-floating-panel>
```

***

### van-loading

**Description**: Loading indicator component.

**Use Cases**:

- Loading states
- Async operation feedback
- Data fetching
- Processing indicators

**Parameters**:

| Parameter  | Type          | Default    | Description             |
| ---------- | ------------- | ---------- | ----------------------- |
| color      | string        | '#c9c9c9'  | Loading color           |
| type       | string        | 'circular' | Type: circular, spinner |
| size       | string/number | '30px'     | Loading size            |
| text-size  | string/number | '14px'     | Text size               |
| vertical   | boolean       | false      | Vertical layout         |
| text-color | string        | '#c9c9c9'  | Text color              |

**Example**:

```vue
<van-loading />
<van-loading type="spinner" color="#1989fa" />
<van-loading size="24px" vertical>Loading...</van-loading>
```

***

### van-notify

**Description**: Notification component for alerts.

**Use Cases**:

- System notifications
- Alert messages
- Status updates
- Quick notifications

**Parameters**:

| Parameter    | Type          | Default  | Description                             |
| ------------ | ------------- | -------- | --------------------------------------- |
| v-model:show | boolean       | false    | Show notify                             |
| type         | string        | 'danger' | Type: primary, success, warning, danger |
| message      | string/number | -        | Message content                         |
| color        | string        | -        | Text color                              |
| background   | string        | -        | Background color                        |
| duration     | number        | 3000     | Display duration                        |
| position     | string        | 'top'    | Position: top, bottom                   |
| z-index      | string/number | -        | z-index                                 |
| teleport     | string        | 'body'   | Teleport target                         |

**Example**:

```vue
<van-notify v-model:show="show" type="success" message="Success!" />

<script setup>
import { showNotify, closeNotify } from 'vant';

showNotify({ type: 'success', message: 'Success!' });
showNotify({ type: 'danger', message: 'Error!' });
</script>
```

***

### van-overlay

**Description**: Overlay mask component.

**Use Cases**:

- Modal overlays
- Loading masks
- Background dimming
- Custom overlays

**Parameters**:

| Parameter    | Type          | Default | Description        |
| ------------ | ------------- | ------- | ------------------ |
| show         | boolean       | false   | Show overlay       |
| z-index      | string/number | 1       | z-index            |
| duration     | string/number | 0.3     | Animation duration |
| class-name   | string        | -       | Custom class       |
| custom-style | object        | -       | Custom style       |
| lock-scroll  | boolean       | true    | Lock body scroll   |
| lazy-render  | boolean       | true    | Lazy render        |
| teleport     | string        | 'body'  | Teleport target    |

**Example**:

```vue
<van-overlay :show="show" @click="show = false">
  <div class="wrapper">
    <div class="block" @click.stop />
  </div>
</van-overlay>
```

***

### van-pull-refresh

**Description**: Pull-down refresh component.

**Use Cases**:

- List refresh
- Content update
- Pull-to-refresh
- Mobile refresh patterns

**Parameters**:

| Parameter          | Type          | Default              | Description        |
| ------------------ | ------------- | -------------------- | ------------------ |
| v-model            | boolean       | false                | Loading state      |
| pulling-text       | string        | 'Pull to refresh'    | Pulling text       |
| loosing-text       | string        | 'Release to refresh' | Loosing text       |
| loading-text       | string        | 'Loading...'         | Loading text       |
| success-text       | string        | -                    | Success text       |
| success-duration   | string/number | 500                  | Success duration   |
| animation-duration | string/number | 300                  | Animation duration |
| head-height        | string/number | 50                   | Head height        |
| pull-distance      | string/number | -                    | Pull distance      |
| disabled           | boolean       | false                | Disabled state     |

**Example**:

```vue
<van-pull-refresh v-model="loading" @refresh="onRefresh">
  <p>Refresh count: {{ count }}</p>
</van-pull-refresh>
```

***

### van-share-sheet

**Description**: Share sheet for sharing content.

**Use Cases**:

- Social sharing
- Content sharing
- Invite friends
- Export options

**Parameters**:

| Parameter    | Type          | Default  | Description        |
| ------------ | ------------- | -------- | ------------------ |
| v-model:show | boolean       | false    | Show share sheet   |
| title        | string        | -        | Title              |
| options      | array         | \[]      | Share options      |
| cancel-text  | string        | 'Cancel' | Cancel button text |
| description  | string        | -        | Description        |
| duration     | string/number | 300      | Animation duration |

**Example**:

```vue
<van-share-sheet
  v-model:show="show"
  title="Share"
  :options="options"
  @select="onSelect"
/>

<script setup>
const options = [
  { name: 'WeChat', icon: 'wechat' },
  { name: 'Weibo', icon: 'weibo' },
  { name: 'Link', icon: 'link' },
  { name: 'QR Code', icon: 'qrcode' }
];
</script>
```

***

### van-swipe-cell

**Description**: Swipeable cell with action buttons.

**Use Cases**:

- Swipe to delete
- Swipe actions
- Quick actions
- List item actions

**Parameters**:

| Parameter        | Type          | Default | Description           |
| ---------------- | ------------- | ------- | --------------------- |
| name             | string/number | -       | Identifier            |
| left-width       | string/number | 'auto'  | Left width            |
| right-width      | string/number | 'auto'  | Right width           |
| left             | array         | -       | Left actions          |
| right            | array         | -       | Right actions         |
| before-close     | function      | -       | Before close callback |
| disabled         | boolean       | false   | Disabled state        |
| stop-propagation | boolean       | false   | Stop propagation      |

**Example**:

```vue
<van-swipe-cell>
  <van-cell title="Cell" value="Content" />
  <template #right>
    <van-button square type="danger" text="Delete" />
  </template>
</van-swipe-cell>
```

***

## Display Components Agents

### van-badge

**Description**: Badge for displaying numbers or status marks.

**Use Cases**:

- Notification counts
- Status indicators
- Unread message badges
- Attention markers

**Parameters**:

| Parameter | Type          | Default     | Description                                              |
| --------- | ------------- | ----------- | -------------------------------------------------------- |
| content   | string/number | -           | Badge content                                            |
| color     | string        | '#ee0a24'   | Badge color                                              |
| dot       | boolean       | false       | Show as dot                                              |
| max       | string/number | -           | Maximum number                                           |
| offset    | array         | -           | Position offset                                          |
| show-zero | boolean       | true        | Show when zero                                           |
| position  | string        | 'top-right' | Position: top-left, top-right, bottom-left, bottom-right |

**Example**:

```vue
<van-badge :content="5">
  <div class="child" />
</van-badge>

<van-badge dot>
  <van-icon name="chat-o" />
</van-badge>
```

***

### van-circle

**Description**: Circular progress indicator.

**Use Cases**:

- Progress display
- Completion indicators
- Circular gauges
- Dashboard metrics

**Parameters**:

| Parameter            | Type          | Default   | Description                              |
| -------------------- | ------------- | --------- | ---------------------------------------- |
| v-model:current-rate | number        | 0         | Current rate                             |
| rate                 | number        | 100       | Target rate                              |
| size                 | string/number | '100px'   | Circle size                              |
| color                | string/object | '#1989fa' | Progress color                           |
| layer-color          | string        | 'white'   | Layer color                              |
| fill                 | string        | 'none'    | Fill color                               |
| speed                | number        | 0         | Animation speed                          |
| text                 | string        | -         | Text                                     |
| stroke-width         | string/number | 40        | Stroke width                             |
| clockwise            | boolean       | true      | Clockwise direction                      |
| start-position       | string        | 'top'     | Start position: top, right, bottom, left |

**Example**:

```vue
<van-circle v-model:current-rate="rate" :rate="30" :speed="100" text="30%" />
<van-circle :rate="rate" color="#07c160" layer-color="#ebedf0" />
```

***

### van-collapse

**Description**: Collapsible accordion panels.

**Use Cases**:

- FAQ sections
- Accordion panels
- Collapsible content
- Expandable lists

**Parameters**:

| Parameter | Type    | Default | Description    |
| --------- | ------- | ------- | -------------- |
| v-model   | array   | -       | Active names   |
| accordion | boolean | false   | Accordion mode |
| border    | boolean | true    | Show border    |

**Example**:

```vue
<van-collapse v-model="activeNames">
  <van-collapse-item title="Title 1" name="1">Content 1</van-collapse-item>
  <van-collapse-item title="Title 2" name="2">Content 2</van-collapse-item>
</van-collapse>
```

***

### van-count-down

**Description**: Countdown timer component.

**Use Cases**:

- Countdown timers
- Time limits
- Expiration displays
- Event countdowns

**Parameters**:

| Parameter   | Type    | Default    | Description         |
| ----------- | ------- | ---------- | ------------------- |
| time        | number  | 0          | Countdown time (ms) |
| format      | string  | 'HH:mm:ss' | Time format         |
| auto-start  | boolean | true       | Auto start          |
| millisecond | boolean | false      | Show milliseconds   |

**Example**:

```vue
<van-count-down :time="30 * 60 * 1000" format="mm:ss" />

<van-count-down :time="time">
  <template #default="timeData">
    <span>{{ timeData.hours }}:{{ timeData.minutes }}:{{ timeData.seconds }}</span>
  </template>
</van-count-down>
```

***

### van-divider

**Description**: Dividing line between content.

**Use Cases**:

- Content separation
- Section dividers
- Visual grouping
- Horizontal rules

**Parameters**:

| Parameter        | Type    | Default  | Description                           |
| ---------------- | ------- | -------- | ------------------------------------- |
| dashed           | boolean | false    | Dashed line                           |
| hairline         | boolean | true     | Hairline style                        |
| content-position | string  | 'center' | Content position: left, center, right |

**Example**:

```vue
<van-divider />
<van-divider>Content</van-divider>
<van-divider content-position="left">Left</van-divider>
<van-divider dashed>Dashed</van-divider>
```

***

### van-empty

**Description**: Empty state placeholder.

**Use Cases**:

- Empty data states
- No search results
- Placeholder content
- Error states

**Parameters**:

| Parameter   | Type          | Default   | Description                            |
| ----------- | ------------- | --------- | -------------------------------------- |
| image       | string        | 'default' | Image: default, error, search, network |
| image-size  | string/number | -         | Image size                             |
| description | string        | -         | Description text                       |

**Example**:

```vue
<van-empty description="No data" />
<van-empty image="search" description="No results found" />
<van-empty image-size="100" description="Custom size" />
```

***

### van-highlight

**Description**: Text highlighting component.

**Use Cases**:

- Search highlighting
- Keyword emphasis
- Text matching
- Result highlighting

**Parameters**:

| Parameter       | Type         | Default | Description           |
| --------------- | ------------ | ------- | --------------------- |
| keywords        | string/array | -       | Keywords to highlight |
| source-string   | string       | -       | Source text           |
| highlight-class | string       | -       | Highlight class       |
| highlight-style | object       | -       | Highlight style       |
| case-sensitive  | boolean      | false   | Case sensitive        |

**Example**:

```vue
<van-highlight :keywords="keyword" :source-string="text" />
```

***

### van-image-preview

**Description**: Image preview with zoom and swipe.

**Use Cases**:

- Image galleries
- Photo previews
- Image zoom
- Swipeable images

**Parameters**:

| Parameter           | Type          | Default     | Description         |
| ------------------- | ------------- | ----------- | ------------------- |
| v-model:show        | boolean       | false       | Show preview        |
| images              | array         | \[]         | Image URLs          |
| start-position      | number        | 0           | Start position      |
| swipe-duration      | number        | 300         | Swipe duration      |
| show-index          | boolean       | true        | Show index          |
| show-indicators     | boolean       | false       | Show indicators     |
| loop                | boolean       | true        | Loop mode           |
| closeable           | boolean       | false       | Show close button   |
| close-icon          | string        | 'cross'     | Close icon          |
| close-icon-position | string        | 'top-right' | Close icon position |
| max-zoom            | string/number | 3           | Maximum zoom        |
| min-zoom            | string/number | 1/3         | Minimum zoom        |

**Example**:

```vue
<van-image-preview v-model:show="show" :images="images" />

<script setup>
import { showImagePreview } from 'vant';

showImagePreview(['image1.jpg', 'image2.jpg']);
</script>
```

***

### van-lazyload

**Description**: Lazy loading directive for images and components.

**Use Cases**:

- Lazy loading images
- Performance optimization
- Deferred loading
- Scroll-based loading

**Example**:

```vue
<img v-lazy="imageUrl" />
<div v-lazy:background-image="imageUrl"></div>
```

***

### van-list

**Description**: Infinite scroll list component.

**Use Cases**:

- Infinite scrolling
- Pagination
- Lazy loading lists
- Load more functionality

**Parameters**:

| Parameter       | Type          | Default      | Description         |
| --------------- | ------------- | ------------ | ------------------- |
| v-model:loading | boolean       | false        | Loading state       |
| v-model:error   | boolean       | false        | Error state         |
| error-text      | string        | -            | Error text          |
| loading-text    | string        | 'Loading...' | Loading text        |
| finished        | boolean       | false        | All data loaded     |
| finished-text   | string        | -            | Finished text       |
| immediate-check | boolean       | true         | Check on mount      |
| offset          | string/number | 300          | Trigger offset      |
| direction       | string        | 'down'       | Direction: up, down |

**Example**:

```vue
<van-list
  v-model:loading="loading"
  :finished="finished"
  finished-text="No more"
  @load="onLoad"
>
  <van-cell v-for="item in list" :key="item" :title="item" />
</van-list>
```

***

### van-notice-bar

**Description**: Scrolling notice bar for announcements.

**Use Cases**:

- Announcements
- Notifications
- Scrolling text
- Alerts

**Parameters**:

| Parameter  | Type          | Default   | Description           |
| ---------- | ------------- | --------- | --------------------- |
| text       | string        | -         | Notice text           |
| mode       | string        | -         | Mode: closeable, link |
| left-icon  | string        | -         | Left icon             |
| right-icon | string        | -         | Right icon            |
| color      | string        | '#f60'    | Text color            |
| background | string        | '#fff7cc' | Background color      |
| delay      | string/number | 1         | Animation delay       |
| speed      | string/number | 60        | Scroll speed          |
| scrollable | boolean       | -         | Auto scroll           |
| wrapable   | boolean       | false     | Allow wrapping        |

**Example**:

```vue
<van-notice-bar text="Important notice message here." />
<van-notice-bar left-icon="volume-o" text="Announcement" />
<van-notice-bar mode="closeable" text="Closeable notice" />
```

***

### van-popover

**Description**: Popover for displaying rich content.

**Use Cases**:

- Rich popups
- Information cards
- Action menus
- Tooltips

**Parameters**:

| Parameter              | Type    | Default    | Description            |
| ---------------------- | ------- | ---------- | ---------------------- |
| v-model:show           | boolean | false      | Show popover           |
| theme                  | string  | 'light'    | Theme: light, dark     |
| trigger                | string  | 'click'    | Trigger: click, manual |
| placement              | string  | 'bottom'   | Placement position     |
| actions                | array   | \[]        | Action items           |
| actions-direction      | string  | 'vertical' | Actions direction      |
| offset                 | array   | \[0, 8]    | Position offset        |
| overlay                | boolean | false      | Show overlay           |
| close-on-click-action  | boolean | true       | Close on action click  |
| close-on-click-outside | boolean | true       | Close on outside click |
| show-arrow             | boolean | true       | Show arrow             |

**Example**:

```vue
<van-popover v-model:show="show" :actions="actions" @select="onSelect">
  <template #reference>
    <van-button type="primary">Show Popover</van-button>
  </template>
</van-popover>
```

***

### van-progress

**Description**: Linear progress bar.

**Use Cases**:

- Progress display
- Upload progress
- Task completion
- Loading states

**Parameters**:

| Parameter    | Type          | Default   | Description         |
| ------------ | ------------- | --------- | ------------------- |
| percentage   | number        | 0         | Progress percentage |
| stroke-width | string/number | '4px'     | Bar height          |
| color        | string/object | '#1989fa' | Progress color      |
| track-color  | string        | '#e5e5e5' | Track color         |
| pivot-text   | string        | -         | Pivot text          |
| pivot-color  | string        | -         | Pivot color         |
| text-color   | string        | 'white'   | Text color          |
| inactive     | boolean       | false     | Inactive state      |
| show-pivot   | boolean       | true      | Show pivot          |

**Example**:

```vue
<van-progress :percentage="50" />
<van-progress :percentage="80" stroke-width="8" color="#07c160" />
<van-progress :percentage="30" pivot-text="Custom" />
```

***

### van-rolling-text

**Description**: Rolling text animation component.

**Use Cases**:

- Number animations
- Rolling text
- Animated counters
- Slot machine effects

**Parameters**:

| Parameter  | Type          | Default | Description          |
| ---------- | ------------- | ------- | -------------------- |
| text       | string/number | -       | Text to display      |
| direction  | string        | 'down'  | Direction: up, down  |
| auto-start | boolean       | true    | Auto start           |
| stop-order | string        | 'ltr'   | Stop order: ltr, rtl |
| height     | string/number | 40      | Item height          |
| duration   | number        | 2       | Animation duration   |

**Example**:

```vue
<van-rolling-text :text="text" />
```

***

### van-skeleton

**Description**: Loading skeleton placeholder.

**Use Cases**:

- Loading states
- Content placeholders
- Perceived performance
- Skeleton screens

**Parameters**:

| Parameter    | Type                | Default | Description                 |
| ------------ | ------------------- | ------- | --------------------------- |
| row          | string/number       | 0       | Number of rows              |
| title        | boolean             | false   | Show title                  |
| avatar       | boolean             | false   | Show avatar                 |
| loading      | boolean             | true    | Loading state               |
| animate      | boolean             | true    | Animation                   |
| round        | boolean             | false   | Round corners               |
| title-width  | string/number       | '40%'   | Title width                 |
| avatar-size  | string/number       | '32px'  | Avatar size                 |
| avatar-shape | string              | 'round' | Avatar shape: round, square |
| row-width    | string/number/array | '100%'  | Row width(s)                |

**Example**:

```vue
<van-skeleton title avatar :row="3" />
<van-skeleton :loading="loading">
  <div>Actual content</div>
</van-skeleton>
```

***

### van-skeleton-avatar

**Description**: Skeleton avatar placeholder.

**Use Cases**:

- Avatar loading placeholders
- Profile loading states

**Parameters**:

| Parameter    | Type          | Default | Description  |
| ------------ | ------------- | ------- | ------------ |
| avatar-size  | string/number | '32px'  | Avatar size  |
| avatar-shape | string        | 'round' | Avatar shape |

**Example**:

```vue
<van-skeleton-avatar />
```

***

### van-skeleton-image

**Description**: Skeleton image placeholder.

**Use Cases**:

- Image loading placeholders
- Gallery loading states

**Parameters**:

| Parameter  | Type          | Default | Description |
| ---------- | ------------- | ------- | ----------- |
| image-size | string/number | '100%'  | Image size  |

**Example**:

```vue
<van-skeleton-image />
```

***

### van-skeleton-paragraph

**Description**: Skeleton paragraph placeholder.

**Use Cases**:

- Text loading placeholders
- Content loading states

**Parameters**:

| Parameter | Type                | Default | Description  |
| --------- | ------------------- | ------- | ------------ |
| row-width | string/number/array | '100%'  | Row width(s) |

**Example**:

```vue
<van-skeleton-paragraph :row-width="['100%', '60%', '80%']" />
```

***

### van-skeleton-title

**Description**: Skeleton title placeholder.

**Use Cases**:

- Title loading placeholders
- Header loading states

**Parameters**:

| Parameter   | Type          | Default | Description |
| ----------- | ------------- | ------- | ----------- |
| title-width | string/number | '40%'   | Title width |

**Example**:

```vue
<van-skeleton-title />
```

***

### van-steps

**Description**: Step-by-step progress indicator.

**Use Cases**:

- Wizard interfaces
- Process workflows
- Step progress
- Checkout flows

**Parameters**:

| Parameter      | Type   | Default      | Description                     |
| -------------- | ------ | ------------ | ------------------------------- |
| active         | number | 0            | Active step                     |
| direction      | string | 'horizontal' | Direction: horizontal, vertical |
| active-icon    | string | 'checked'    | Active icon                     |
| active-color   | string | '#07c160'    | Active color                    |
| inactive-icon  | string | -            | Inactive icon                   |
| inactive-color | string | '#969799'    | Inactive color                  |

**Example**:

```vue
<van-steps :active="active">
  <van-step>Step 1</van-step>
  <van-step>Step 2</van-step>
  <van-step>Step 3</van-step>
</van-steps>
```

***

### van-sticky

**Description**: Sticky positioning component.

**Use Cases**:

- Sticky headers
- Fixed toolbars
- Persistent navigation
- Scroll-based positioning

**Parameters**:

| Parameter     | Type        | Default | Description           |
| ------------- | ----------- | ------- | --------------------- |
| position      | string      | 'top'   | Position: top, bottom |
| offset-top    | number      | 0       | Top offset            |
| offset-bottom | number      | 0       | Bottom offset         |
| z-index       | number      | 99      | z-index               |
| container     | HTMLElement | -       | Container element     |

**Example**:

```vue
<van-sticky>
  <van-nav-bar title="Sticky Header" />
</van-sticky>
```

***

### van-swipe

**Description**: Swipeable carousel component.

**Use Cases**:

- Image carousels
- Content sliders
- Banner rotations
- Product showcases

**Parameters**:

| Parameter        | Type    | Default   | Description        |
| ---------------- | ------- | --------- | ------------------ |
| v-model:active   | number  | 0         | Active index       |
| autoplay         | number  | -         | Auto play interval |
| duration         | number  | 500       | Animation duration |
| initial-swipe    | number  | 0         | Initial index      |
| loop             | boolean | true      | Loop mode          |
| show-indicators  | boolean | true      | Show indicators    |
| indicator-color  | string  | '#1989fa' | Indicator color    |
| vertical         | boolean | false     | Vertical mode      |
| touchable        | boolean | true      | Touch support      |
| stop-propagation | boolean | true      | Stop propagation   |
| lazy-render      | boolean | false     | Lazy render        |

**Example**:

```vue
<van-swipe :autoplay="3000" indicator-color="white">
  <van-swipe-item v-for="image in images" :key="image">
    <img :src="image" />
  </van-swipe-item>
</van-swipe>
```

***

### van-tag

**Description**: Tag for labels and categorization.

**Use Cases**:

- Category labels
- Status tags
- Product tags
- Filter markers

**Parameters**:

| Parameter  | Type    | Default   | Description                                      |
| ---------- | ------- | --------- | ------------------------------------------------ |
| type       | string  | 'default' | Type: primary, success, danger, warning, default |
| size       | string  | -         | Size: large, medium, small                       |
| color      | string  | -         | Custom color                                     |
| text-color | string  | 'white'   | Text color                                       |
| plain      | boolean | false     | Plain style                                      |
| round      | boolean | false     | Round corners                                    |
| mark       | boolean | false     | Mark style                                       |
| show       | boolean | true      | Show tag                                         |
| closeable  | boolean | false     | Show close button                                |

**Example**:

```vue
<van-tag type="primary">Primary</van-tag>
<van-tag type="success" plain>Plain Success</van-tag>
<van-tag closeable @close="onClose">Closeable</van-tag>
```

***

### van-text-ellipsis

**Description**: Text truncation with expand/collapse.

**Use Cases**:

- Text truncation
- Expandable text
- Content previews
- Long text handling

**Parameters**:

| Parameter     | Type          | Default    | Description                  |
| ------------- | ------------- | ---------- | ---------------------------- |
| text          | string        | -          | Text content                 |
| rows          | string/number | 1          | Maximum rows                 |
| expand-text   | string        | 'Expand'   | Expand text                  |
| collapse-text | string        | 'Collapse' | Collapse text                |
| dots          | string        | '...'      | Dots text                    |
| position      | string        | 'end'      | Position: start, middle, end |

**Example**:

```vue
<van-text-ellipsis :text="longText" :rows="2" />
<van-text-ellipsis :text="longText" expand-text="More" collapse-text="Less" />
```

***

### van-watermark

**Description**: Watermark overlay component.

**Use Cases**:

- Content protection
- Branding
- Copyright notices
- Security marks

**Parameters**:

| Parameter    | Type          | Default   | Description      |
| ------------ | ------------- | --------- | ---------------- |
| content      | string/array  | -         | Watermark text   |
| width        | number        | 100       | Watermark width  |
| height       | number        | 100       | Watermark height |
| rotate       | number        | -22       | Rotation angle   |
| image        | string        | -         | Image URL        |
| image-width  | number        | -         | Image width      |
| image-height | number        | -         | Image height     |
| z-index      | number        | 100       | z-index          |
| gap-x        | number        | 0         | Horizontal gap   |
| gap-y        | number        | 0         | Vertical gap     |
| font-color   | string        | '#dcdee0' | Font color       |
| font-size    | string/number | -         | Font size        |
| opacity      | string/number | -         | Opacity          |

**Example**:

```vue
<van-watermark content="Vant">
  <div style="height: 300px">Content</div>
</van-watermark>
```

***

## Navigation Components Agents

### van-action-bar

**Description**: Bottom action bar for page actions.

**Use Cases**:

- Shopping cart actions
- Form submissions
- Bottom toolbars
- Action buttons

**Parameters**:

| Parameter              | Type    | Default | Description      |
| ---------------------- | ------- | ------- | ---------------- |
| safe-area-inset-bottom | boolean | true    | Enable safe area |
| placeholder            | boolean | false   | Show placeholder |

**Example**:

```vue
<van-action-bar>
  <van-action-bar-icon icon="chat-o" text="Chat" />
  <van-action-bar-icon icon="cart-o" text="Cart" badge="5" />
  <van-action-bar-button type="warning" text="Add to Cart" />
  <van-action-bar-button type="danger" text="Buy Now" />
</van-action-bar>
```

***

### van-back-top

**Description**: Back to top button for long pages.

**Use Cases**:

- Long page navigation
- Quick scroll to top
- Improved UX
- Scroll to top

**Parameters**:

| Parameter         | Type          | Default | Description        |
| ----------------- | ------------- | ------- | ------------------ |
| target            | string        | -       | Target element     |
| visibility-height | number        | 200     | Min height to show |
| bottom            | string/number | 30      | Bottom distance    |
| right             | string/number | 30      | Right distance     |
| z-index           | string/number | 100     | z-index            |
| teleport          | string        | 'body'  | Teleport target    |
| immediate         | boolean       | false   | Immediate scroll   |

**Example**:

```vue
<van-back-top />
<van-back-top bottom="50" right="20">
  <van-icon name="back-top" />
</van-back-top>
```

***

### van-grid

**Description**: Grid layout for icons and content.

**Use Cases**:

- Icon grids
- Feature lists
- Dashboard layouts
- Menu grids

**Parameters**:

| Parameter  | Type          | Default    | Description                     |
| ---------- | ------------- | ---------- | ------------------------------- |
| column-num | string/number | 4          | Columns per row                 |
| icon-size  | string/number | '28px'     | Icon size                       |
| gutter     | string/number | 0          | Gap between items               |
| border     | boolean       | true       | Show border                     |
| center     | boolean       | true       | Center content                  |
| square     | boolean       | false      | Square items                    |
| clickable  | boolean       | false      | Enable click feedback           |
| direction  | string        | 'vertical' | Direction: vertical, horizontal |

**Example**:

```vue
<van-grid :column-num="3">
  <van-grid-item icon="photo-o" text="Photo" />
  <van-grid-item icon="video-o" text="Video" />
  <van-grid-item icon="music-o" text="Music" />
</van-grid>
```

***

### van-index-bar

**Description**: Alphabetical index bar for quick navigation.

**Use Cases**:

- Contact lists
- City selection
- Alphabetical navigation
- Quick access lists

**Parameters**:

| Parameter         | Type    | Default   | Description     |
| ----------------- | ------- | --------- | --------------- |
| sticky            | boolean | true      | Sticky anchors  |
| sticky-offset-top | number  | 0         | Sticky offset   |
| highlight-color   | string  | '#07c160' | Highlight color |
| index-list        | array   | -         | Index list      |

**Example**:

```vue
<van-index-bar>
  <van-index-anchor index="A" />
  <van-cell title="Apple" />
  <van-cell title="Avocado" />
  <van-index-anchor index="B" />
  <van-cell title="Banana" />
</van-index-bar>
```

***

### van-nav-bar

**Description**: Navigation bar for page headers.

**Use Cases**:

- Page headers
- Navigation controls
- Back buttons
- Title displays

**Parameters**:

| Parameter           | Type          | Default | Description           |
| ------------------- | ------------- | ------- | --------------------- |
| title               | string        | -       | Title                 |
| left-text           | string        | -       | Left text             |
| right-text          | string        | -       | Right text            |
| left-arrow          | boolean       | false   | Show left arrow       |
| border              | boolean       | true    | Show border           |
| fixed               | boolean       | false   | Fixed position        |
| placeholder         | boolean       | false   | Show placeholder      |
| z-index             | string/number | 1       | z-index               |
| safe-area-inset-top | boolean       | false   | Enable safe area      |
| clickable           | boolean       | true    | Enable click feedback |

**Example**:

```vue
<van-nav-bar title="Title" left-arrow @click-left="onClickLeft" />

<van-nav-bar
  title="Title"
  left-text="Back"
  right-text="Button"
  left-arrow
  @click-left="onClickLeft"
  @click-right="onClickRight"
/>
```

***

### van-pagination

**Description**: Pagination for navigating pages.

**Use Cases**:

- Page navigation
- Data pagination
- List navigation
- Content browsing

**Parameters**:

| Parameter        | Type          | Default | Description          |
| ---------------- | ------------- | ------- | -------------------- |
| v-model          | number        | -       | Current page         |
| mode             | string        | 'multi' | Mode: multi, simple  |
| prev-text        | string        | -       | Previous text        |
| next-text        | string        | -       | Next text            |
| page-count       | string/number | -       | Total pages          |
| total-items      | string/number | -       | Total items          |
| items-per-page   | string/number | 10      | Items per page       |
| show-page-size   | string/number | 5       | Visible page buttons |
| force-ellipses   | boolean       | false   | Force ellipses       |
| show-prev-button | boolean       | true    | Show previous button |
| show-next-button | boolean       | true    | Show next button     |

**Example**:

```vue
<van-pagination v-model="page" :total-items="24" :items-per-page="5" />
<van-pagination v-model="page" mode="simple" :page-count="12" />
```

***

### van-sidebar

**Description**: Side navigation sidebar.

**Use Cases**:

- Side navigation
- Category navigation
- Settings menus
- Tab navigation

**Parameters**:

| Parameter | Type   | Default | Description  |
| --------- | ------ | ------- | ------------ |
| v-model   | number | 0       | Active index |

**Example**:

```vue
<van-sidebar v-model="active">
  <van-sidebar-item title="Category 1" />
  <van-sidebar-item title="Category 2" />
  <van-sidebar-item title="Category 3" />
</van-sidebar>
```

***

### van-tab

**Description**: Tab component for tabbed content.

**Use Cases**:

- Tabbed content
- Content organization
- Multi-panel interfaces
- Category switching

**Parameters**:

| Parameter      | Type          | Default | Description        |
| -------------- | ------------- | ------- | ------------------ |
| v-model:active | string/number | 0       | Active tab         |
| type           | string        | 'line'  | Type: line, card   |
| color          | string        | -       | Theme color        |
| background     | string        | -       | Background color   |
| duration       | string/number | 0.3     | Animation duration |
| line-width     | string/number | '40px'  | Line width         |
| line-height    | string/number | '3px'   | Line height        |
| animated       | boolean       | false   | Animate content    |
| border         | boolean       | false   | Show border        |
| ellipsis       | boolean       | true    | Ellipsis text      |
| sticky         | boolean       | false   | Sticky mode        |
| swipeable      | boolean       | false   | Swipe support      |
| scrollspy      | boolean       | false   | Scroll spy         |
| offset-top     | number        | 0       | Sticky offset      |
| shrink         | boolean       | false   | Shrink tabs        |
| lazy-render    | boolean       | true    | Lazy render        |

**Example**:

```vue
<van-tabs v-model:active="active">
  <van-tab title="Tab 1">Content 1</van-tab>
  <van-tab title="Tab 2">Content 2</van-tab>
  <van-tab title="Tab 3">Content 3</van-tab>
</van-tabs>
```

***

### van-tabbar

**Description**: Bottom tab bar for main navigation.

**Use Cases**:

- Main navigation
- Bottom tabs
- App navigation
- Page switching

**Parameters**:

| Parameter              | Type          | Default   | Description      |
| ---------------------- | ------------- | --------- | ---------------- |
| v-model                | number        | 0         | Active index     |
| fixed                  | boolean       | true      | Fixed position   |
| border                 | boolean       | true      | Show border      |
| z-index                | string/number | 1         | z-index          |
| active-color           | string        | '#1989fa' | Active color     |
| inactive-color         | string        | '#646566' | Inactive color   |
| route                  | boolean       | false     | Route mode       |
| placeholder            | boolean       | false     | Show placeholder |
| safe-area-inset-bottom | boolean       | false     | Enable safe area |

**Example**:

```vue
<van-tabbar v-model="active">
  <van-tabbar-item icon="home-o">Home</van-tabbar-item>
  <van-tabbar-item icon="search">Search</van-tabbar-item>
  <van-tabbar-item icon="friends-o">Friends</van-tabbar-item>
  <van-tabbar-item icon="setting-o">Settings</van-tabbar-item>
</van-tabbar>
```

***

### van-tree-select

**Description**: Tree selection for hierarchical data.

**Use Cases**:

- Category selection
- Hierarchical navigation
- Multi-level selection
- Product categories

**Parameters**:

| Parameter                 | Type                | Default  | Description          |
| ------------------------- | ------------------- | -------- | -------------------- |
| v-model:active-id         | string/number/array | -        | Active right item(s) |
| v-model:main-active-index | number              | -        | Active left index    |
| items                     | array               | \[]      | Items data           |
| height                    | string/number       | 300      | Component height     |
| max                       | string/number       | Infinity | Max selected items   |

**Example**:

```vue
<van-tree-select
  v-model:active-id="activeId"
  v-model:main-active-index="activeIndex"
  :items="items"
/>

<script setup>
const items = [
  {
    text: 'Group 1',
    children: [
      { text: 'Item 1', id: 1 },
      { text: 'Item 2', id: 2 }
    ]
  }
];
</script>
```

***

## Business Components Agents

### van-address-edit

**Description**: Address editing form component.

**Use Cases**:

- Address management
- Shipping address forms
- Address editing
- Location input

**Parameters**:

| Parameter                | Type          | Default | Description        |
| ------------------------ | ------------- | ------- | ------------------ |
| area-list                | object        | -       | Area data          |
| is-saving                | boolean       | false   | Saving state       |
| is-deleting              | boolean       | false   | Deleting state     |
| validator                | function      | -       | Custom validator   |
| show-delete              | boolean       | false   | Show delete button |
| show-set-default         | boolean       | false   | Show set default   |
| show-search-result       | boolean       | true    | Show search result |
| save-button-text         | string        | -       | Save button text   |
| delete-button-text       | string        | -       | Delete button text |
| detail-rows              | string/number | 1       | Detail rows        |
| detail-maxlength         | string/number | 200     | Detail max length  |
| search-result            | array         | \[]     | Search results     |
| tel-validator            | function      | -       | Tel validator      |
| postal-validator         | function      | -       | Postal validator   |
| area-columns-placeholder | array         | \[]     | Area placeholder   |

**Example**:

```vue
<van-address-edit
  :area-list="areaList"
  :address-info="addressInfo"
  @save="onSave"
  @delete="onDelete"
/>
```

***

### van-address-list

**Description**: Address list for displaying addresses.

**Use Cases**:

- Address management
- Address selection
- Shipping address list
- Location management

**Parameters**:

| Parameter        | Type          | Default | Description         |
| ---------------- | ------------- | ------- | ------------------- |
| v-model          | string/number | -       | Selected address id |
| list             | array         | \[]     | Address list        |
| disabled-list    | array         | \[]     | Disabled addresses  |
| disabled-text    | string        | -       | Disabled text       |
| switchable       | boolean       | true    | Allow switching     |
| default-tag-text | string        | -       | Default tag text    |
| add-button-text  | string        | 'Add'   | Add button text     |

**Example**:

```vue
<van-address-list
  v-model="chosenAddressId"
  :list="list"
  @add="onAdd"
  @edit="onEdit"
  @select="onSelect"
/>
```

***

### van-area

**Description**: Area/region selection component.

**Use Cases**:

- Region selection
- Province/city/district selection
- Address input
- Location selection

**Parameters**:

| Parameter           | Type          | Default | Description        |
| ------------------- | ------------- | ------- | ------------------ |
| v-model             | string        | -       | Area code          |
| title               | string        | -       | Picker title       |
| area-list           | object        | -       | Area data          |
| columns-num         | string/number | 3       | Column count       |
| columns-placeholder | array         | \[]     | Column placeholder |
| loading             | boolean       | false   | Loading state      |
| readonly            | boolean       | false   | Readonly state     |
| item-height         | string/number | 44      | Item height        |
| visible-item-count  | string/number | 6       | Visible items      |
| swipe-duration      | string/number | 1000    | Swipe duration     |

**Example**:

```vue
<van-area
  v-model="code"
  title="Select Area"
  :area-list="areaList"
  @confirm="onConfirm"
/>
```

***

### van-card

**Description**: Card component for product display.

**Use Cases**:

- Product cards
- Item displays
- Shopping cart items
- Order items

**Parameters**:

| Parameter    | Type          | Default     | Description     |
| ------------ | ------------- | ----------- | --------------- |
| title        | string        | -           | Product title   |
| desc         | string        | -           | Description     |
| thumb        | string        | -           | Image URL       |
| thumb-link   | string        | -           | Image link      |
| tag          | string        | -           | Tag text        |
| price        | string/number | -           | Price           |
| origin-price | string/number | -           | Original price  |
| num          | string/number | -           | Quantity        |
| currency     | string        | '¥'         | Currency symbol |
| centered     | boolean       | false       | Center content  |
| lazy-load    | boolean       | false       | Lazy load image |
| thumb-mode   | string        | 'aspectFit' | Image fit mode  |
| thumb-ratio  | string        | '1:1'       | Image ratio     |

**Example**:

```vue
<van-card
  title="Product Title"
  desc="Description"
  price="100.00"
  thumb="image.jpg"
/>
```

***

### van-contact-card

**Description**: Contact card for displaying contact info.

**Use Cases**:

- Contact display
- User information
- Profile cards
- Contact selection

**Parameters**:

| Parameter | Type    | Default       | Description     |
| --------- | ------- | ------------- | --------------- |
| type      | string  | 'add'         | Type: add, edit |
| name      | string  | -             | Contact name    |
| tel       | string  | -             | Contact phone   |
| add-text  | string  | 'Add Contact' | Add text        |
| editable  | boolean | true          | Editable        |

**Example**:

```vue
<van-contact-card type="add" @click="onAdd" />
<van-contact-card type="edit" name="John" tel="1234567890" @click="onEdit" />
```

***

### van-contact-edit

**Description**: Contact editing form.

**Use Cases**:

- Contact management
- Contact editing
- Contact creation
- Address book

**Parameters**:

| Parameter          | Type     | Default | Description        |
| ------------------ | -------- | ------- | ------------------ |
| contact-info       | object   | -       | Contact info       |
| is-edit            | boolean  | false   | Edit mode          |
| is-saving          | boolean  | false   | Saving state       |
| is-deleting        | boolean  | false   | Deleting state     |
| show-set-default   | boolean  | false   | Show set default   |
| set-default-label  | string   | -       | Default label      |
| save-button-text   | string   | -       | Save button text   |
| delete-button-text | string   | -       | Delete button text |
| tel-validator      | function | -       | Tel validator      |

**Example**:

```vue
<van-contact-edit
  :contact-info="contact"
  @save="onSave"
  @delete="onDelete"
/>
```

***

### van-contact-list

**Description**: Contact list for displaying contacts.

**Use Cases**:

- Contact management
- Contact selection
- Address book
- User lists

**Parameters**:

| Parameter       | Type          | Default | Description         |
| --------------- | ------------- | ------- | ------------------- |
| v-model         | string/number | -       | Selected contact id |
| list            | array         | \[]     | Contact list        |
| add-button-text | string        | 'Add'   | Add button text     |

**Example**:

```vue
<van-contact-list
  v-model="contactId"
  :list="list"
  @add="onAdd"
  @edit="onEdit"
  @select="onSelect"
/>
```

***

### van-coupon-list

**Description**: Coupon list for displaying and selecting coupons.

**Use Cases**:

- Coupon selection
- Discount management
- Promotion display
- Coupon management

**Parameters**:

| Parameter                | Type          | Default       | Description           |
| ------------------------ | ------------- | ------------- | --------------------- |
| v-model                  | number        | -             | Selected coupon index |
| coupons                  | array         | \[]           | Available coupons     |
| disabled-coupons         | array         | \[]           | Disabled coupons      |
| enabled-title            | string        | 'Available'   | Enabled title         |
| disabled-title           | string        | 'Unavailable' | Disabled title        |
| exchange-button-disabled | boolean       | false         | Disable exchange      |
| exchange-button-loading  | boolean       | false         | Exchange loading      |
| exchange-button-text     | string        | 'Exchange'    | Exchange text         |
| exchange-min-length      | string/number | 1             | Min code length       |
| displayed-coupon-index   | number        | -             | Displayed index       |
| show-close-button        | boolean       | true          | Show close button     |
| show-exchange-bar        | boolean       | true          | Show exchange bar     |
| show-count               | boolean       | true          | Show coupon count     |
| currency                 | string        | '¥'           | Currency symbol       |
| empty-image              | string        | -             | Empty image           |

**Example**:

```vue
<van-coupon-list
  :coupons="coupons"
  :disabled-coupons="disabledCoupons"
  @change="onChange"
  @exchange="onExchange"
/>
```

***

### van-submit-bar

**Description**: Submit bar for checkout and order submission.

**Use Cases**:

- Shopping cart checkout
- Order submission
- Payment bars
- Action bars

**Parameters**:

| Parameter              | Type          | Default  | Description         |
| ---------------------- | ------------- | -------- | ------------------- |
| price                  | number        | -        | Total price (cents) |
| decimal-length         | string/number | 2        | Decimal places      |
| label                  | string        | -        | Price label         |
| suffix-label           | string        | -        | Suffix label        |
| text-align             | string        | 'right'  | Text alignment      |
| button-text            | string        | -        | Button text         |
| button-type            | string        | 'danger' | Button type         |
| button-color           | string        | -        | Button color        |
| tip                    | string        | -        | Tip text            |
| tip-icon               | string        | -        | Tip icon            |
| currency               | string        | '¥'      | Currency symbol     |
| disabled               | boolean       | false    | Disabled state      |
| loading                | boolean       | false    | Loading state       |
| safe-area-inset-bottom | boolean       | true     | Enable safe area    |
| placeholder            | boolean       | false    | Show placeholder    |
| decimal                | boolean       | true     | Show decimal        |

**Example**:

```vue
<van-submit-bar
  :price="3050"
  button-text="Submit"
  @submit="onSubmit"
>
  <van-checkbox v-model="checked">Check</van-checkbox>
  <template #tip>
    <div>Tip content</div>
  </template>
</van-submit-bar>
```

***

## Composables Agents

### useCountDown

**Description**: Countdown timer composable.

**Use Cases**:

- Countdown timers
- Time limits
- Expiration tracking
- Event countdowns

**Parameters**:

| Parameter   | Type     | Default    | Description       |
| ----------- | -------- | ---------- | ----------------- |
| time        | number   | 0          | Total time (ms)   |
| autostart   | boolean  | true       | Auto start        |
| format      | string   | 'HH:mm:ss' | Time format       |
| millisecond | boolean  | false      | Show milliseconds |
| onFinish    | function | -          | Finish callback   |
| onChange    | function | -          | Change callback   |

**Example**:

```vue
<script setup>
import { useCountDown } from '@vant/use';

const countDown = useCountDown({
  time: 60 * 1000,
  onFinish: () => console.log('Finished')
});

countDown.start();
</script>

<template>
  <span>{{ countDown.current }}</span>
</template>
```

***

### useRect

**Description**: Get element bounding rect.

**Use Cases**:

- Element dimensions
- Position calculations
- Layout measurements
- Scroll positions

**Example**:

```vue
<script setup>
import { useRect } from '@vant/use';

const root = ref();
const rect = useRect(root);
</script>

<template>
  <div ref="root">Element</div>
</template>
```

***

### useWindowSize

**Description**: Get window size reactively.

**Use Cases**:

- Responsive design
- Window dimensions
- Layout calculations
- Viewport tracking

**Example**:

```vue
<script setup>
import { useWindowSize } from '@vant/use';

const { width, height } = useWindowSize();
</script>

<template>
  <div>Width: {{ width }}, Height: {{ height }}</div>
</template>
```

***

### useScrollParent

**Description**: Get scrollable parent element.

**Use Cases**:

- Scroll detection
- Scroll containers
- Parent scrolling
- Scroll events

**Example**:

```vue
<script setup>
import { useScrollParent } from '@vant/use';

const root = ref();
const scrollParent = useScrollParent(root);
</script>
```

***

### useEventListener

**Description**: Add event listener with auto cleanup.

**Use Cases**:

- Event handling
- DOM events
- Window events
- Custom events

**Example**:

```vue
<script setup>
import { useEventListener } from '@vant/use';

useEventListener('resize', () => {
  console.log('Window resized');
});
</script>
```

***

### usePageVisibility

**Description**: Track page visibility state.

**Use Cases**:

- Page visibility
- Tab switching
- Background detection
- Visibility events

**Example**:

```vue
<script setup>
import { usePageVisibility } from '@vant/use';

const pageVisibility = usePageVisibility();
</script>

<template>
  <div>Page visible: {{ pageVisibility.value }}</div>
</template>
```

***

### useCustomFieldValue

**Description**: Custom form field value management.

**Use Cases**:

- Custom form fields
- Form validation
- Field value binding
- Custom inputs

**Example**:

```vue
<script setup>
import { useCustomFieldValue } from '@vant/use';

useCustomFieldValue(() => customValue.value);
</script>
```

***

### useRelation

**Description**: Parent-child component relationship management.

**Use Cases**:

- Component relationships
- Parent-child binding
- Component hierarchy
- Data propagation

**Example**:

```vue
<script setup>
import { useRelation } from '@vant/use';

const { link, unlink, children } = useRelation('van-checkbox-group');
</script>
```

***

### useToggle

**Description**: Toggle boolean state.

**Use Cases**:

- Toggle states
- Boolean switching
- Show/hide logic
- On/off states

**Example**:

```vue
<script setup>
import { useToggle } from '@vant/use';

const [show, toggle] = useToggle();
</script>

<template>
  <button @click="toggle()">{{ show ? 'Hide' : 'Show' }}</button>
</template>
```

***

### useClickAway

**Description**: Detect clicks outside an element.

**Use Cases**:

- Click outside detection
- Dropdown dismissal
- Modal closing
- Popup dismissal

**Parameters**:

| Parameter         | Type              | Default | Description       |
| ----------------- | ----------------- | ------- | ----------------- |
| target            | Element/Ref/Array | -       | Target element(s) |
| listener          | EventListener     | -       | Callback function |
| options.eventName | string            | 'click' | Event type        |

**Example**:

```vue
<script setup>
import { ref } from 'vue';
import { useClickAway } from '@vant/use';

const dropdown = ref();

useClickAway(dropdown, () => {
  isOpen.value = false;
});
</script>

<template>
  <div ref="dropdown" class="dropdown">Dropdown content</div>
</template>
```

***

### useRaf

**Description**: requestAnimationFrame wrapper for smooth animations.

**Use Cases**:

- Smooth animations
- Game loops
- Visual updates
- Canvas rendering

**Parameters**:

| Parameter        | Type     | Default | Description                 |
| ---------------- | -------- | ------- | --------------------------- |
| callback         | function | -       | Function to execute         |
| options.interval | number   | 0       | Time between calls (ms)     |
| options.isLoop   | boolean  | false   | Enable continuous execution |

**Returns**: Cancel function

**Example**:

```vue
<script setup>
import { ref, onUnmounted } from 'vue';
import { useRaf } from '@vant/use';

const position = ref(0);
let cancel = null;

const animate = () => {
  position.value = (position.value + 2) % 300;
  cancel = useRaf(animate);
};

onUnmounted(() => cancel?.());
</script>

<template>
  <div :style="{ transform: `translateX(${position}px)` }" />
</template>
```

***

## Foundation Agents

Foundation skills provide essential setup and configuration guidance for Vant projects.

### vant-quickstart

**Description**: Setup and configure Vant in Vue 3 projects.

**Use Cases**:

- Installing Vant in new projects
- Configuring import methods
- Framework integration (Vite, Nuxt, Webpack)
- Project initialization

**Key Features**:

- Package manager installation (npm, yarn, pnpm, bun)
- CDN import for prototyping
- Basic usage with Tree Shaking
- On-demand import with unplugin
- Nuxt 3 integration

**Example**:

```bash
npm i vant
```

```js
import { createApp } from 'vue';
import { Button } from 'vant';
import 'vant/lib/index.css';

const app = createApp();
app.use(Button);
```

***

### vant-theming

**Description**: Customize Vant themes using CSS Variables and ConfigProvider.

**Use Cases**:

- Custom color schemes
- Dark mode implementation
- Component style overrides
- Brand customization

**Key Features**:

- CSS Variables override
- ConfigProvider theme configuration
- Dark mode support
- Theme-specific variables

**Example**:

```vue
<van-config-provider :theme-vars="themeVars" theme="dark">
  <van-button type="primary">Themed Button</van-button>
</van-config-provider>

<script setup>
const themeVars = {
  buttonPrimaryBackground: '#07c160',
  buttonPrimaryBorderColor: '#07c160'
};
</script>
```

***

### vant-i18n

**Description**: Configure internationalization in Vant projects.

**Use Cases**:

- Language switching
- Custom translations
- Multi-language support
- Locale management

**Key Features**:

- 40+ supported languages
- Custom language packs
- Vue I18n integration
- Dynamic language switching

**Example**:

```js
import { Locale } from 'vant';
import enUS from 'vant/es/locale/lang/en-US';

Locale.use('en-US', enUS);
```

***

### vant-advanced-usage

**Description**: Advanced usage patterns including component registration and browser adaptation.

**Use Cases**:

- Component registration methods
- Browser adaptation (vw/vh/rem)
- PC browser support
- Performance optimization

**Key Features**:

- Global/local registration
- Viewport unit conversion
- Touch emulator for PC
- Built-in utility styles

**Example**:

```js
// PC browser support
import '@vant/touch-emulator';

// PostCSS config for rem
module.exports = {
  plugins: {
    'postcss-pxtorem': {
      rootValue: 37.5,
      propList: ['*'],
    },
  },
};
```

***

### vant-components

**Description**: Overview of all Vant components organized by category.

**Use Cases**:

- Component exploration
- Finding the right component
- Quick reference
- Component category lookup

**Key Features**:

- 6 component categories
- 86+ components documented
- Quick selection guide
- Common props patterns

**Categories**:

- Basic Components (10)
- Form Components (19)
- Action Components (12)
- Display Components (26)
- Navigation Components (10)
- Business Components (9)

***

### vant-composables

**Description**: Overview of all Vant composables (Vue 3 composition API utilities).

**Use Cases**:

- Composable exploration
- Finding the right composable
- Vue 3 patterns
- Reusable logic

**Key Features**:

- 11 composables documented
- Category organization
- API summary
- Usage patterns

**Categories**:

- State Management (useToggle, useCountDown)
- Event Handling (useClickAway, useEventListener)
- DOM & Layout (useRect, useWindowSize, useScrollParent)
- Lifecycle & Performance (useRaf, usePageVisibility)
- Component Relations (useRelation, useCustomFieldValue)

&#x20;

