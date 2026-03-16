---
name: "vant-components"
description: "Provides an overview of all Vant components organized by category. Invoke when user needs to explore available components or find the right component for their use case."
metadata:
  author: jiaiyan
  version: "1.0.0"
---

# Vant Components Overview

This skill provides a comprehensive overview of all Vant components organized by category, helping developers find the right component for their needs.

## When to Invoke

Invoke this skill when:
- User wants to explore available Vant components
- User needs to find a component for a specific use case
- User asks about component categories
- User wants a quick reference of all components

## Component Categories

### Basic Components

Essential building blocks for any application.

| Component | Description |
|-----------|-------------|
| Button | Trigger actions like form submission |
| Cell | Display information in a list format |
| Icon | Display icons |
| Image | Display images with lazy loading support |
| Popup | Display content in a popup layer |
| Space | Add spacing between elements |
| Toast | Display lightweight feedback messages |
| ConfigProvider | Global configuration for components |
| Col | Column layout component |
| Style | Built-in utility styles |

### Form Components

Components for collecting user input.

| Component | Description |
|-----------|-------------|
| Calendar | Date selection calendar |
| Cascader | Cascading selection |
| Checkbox | Multiple selection |
| DatePicker | Date picker |
| Field | Input field for forms |
| Form | Form validation and submission |
| NumberKeyboard | Numeric input keyboard |
| PasswordInput | Password input display |
| Picker | General picker component |
| PickerGroup | Group multiple pickers |
| Radio | Single selection |
| Rate | Star rating |
| Search | Search input |
| Signature | Signature capture |
| Slider | Slider for value selection |
| Stepper | Numeric stepper |
| Switch | Toggle switch |
| TimePicker | Time picker |
| Uploader | File upload |

### Action Components

Components for user interactions.

| Component | Description |
|-----------|-------------|
| ActionSheet | Action selection panel |
| Barrage | Barrage/danmu display |
| Dialog | Modal dialog |
| DropdownMenu | Dropdown menu |
| FloatingBubble | Floating bubble button |
| FloatingPanel | Floating panel |
| Loading | Loading indicator |
| Notify | Notification message |
| Overlay | Overlay layer |
| PullRefresh | Pull to refresh |
| ShareSheet | Share action sheet |
| SwipeCell | Swipeable cell |

### Display Components

Components for displaying content.

| Component | Description |
|-----------|-------------|
| Badge | Badge or status indicator |
| Circle | Circular progress indicator |
| Collapse | Collapsible content panels |
| CountDown | Countdown timer |
| Divider | Content divider |
| Empty | Empty state placeholder |
| Highlight | Text highlighting |
| ImagePreview | Image preview gallery |
| Lazyload | Lazy loading directive |
| List | Infinite scroll list |
| NoticeBar | Scrolling notice bar |
| Popover | Popup bubble |
| Progress | Progress bar |
| RollingText | Rolling text animation |
| Skeleton | Loading skeleton |
| SkeletonAvatar | Avatar skeleton |
| SkeletonImage | Image skeleton |
| SkeletonParagraph | Paragraph skeleton |
| SkeletonTitle | Title skeleton |
| Steps | Step indicator |
| Sticky | Sticky positioning |
| Swipe | Swipe carousel |
| Tag | Tag or label |
| TextEllipsis | Text truncation |
| Watermark | Watermark overlay |

### Navigation Components

Components for navigation and routing.

| Component | Description |
|-----------|-------------|
| ActionBar | Bottom action bar |
| BackTop | Back to top button |
| Grid | Grid layout |
| IndexBar | A-Z index bar |
| NavBar | Navigation bar |
| Pagination | Pagination controls |
| Sidebar | Side navigation |
| Tab | Tab navigation |
| Tabbar | Bottom tab bar |
| TreeSelect | Tree selection |

### Business Components

Pre-built components for common business scenarios.

| Component | Description |
|-----------|-------------|
| AddressEdit | Address editing form |
| AddressList | Address list |
| Area | Area/region selection |
| Card | Product card |
| ContactCard | Contact card display |
| ContactEdit | Contact editing form |
| ContactList | Contact list |
| CouponList | Coupon list |
| SubmitBar | Order submit bar |

### Composables

Vue 3 composition API utilities.

| Composable | Description |
|------------|-------------|
| useClickAway | Detect clicks outside element |
| useCountDown | Countdown logic |
| useCustomFieldValue | Custom form field value |
| useEventListener | Event listener |
| usePageVisibility | Page visibility detection |
| useRaf | RequestAnimationFrame |
| useRect | Element bounding rect |
| useRelation | Parent-child relation |
| useScrollParent | Scroll parent detection |
| useToggle | Toggle boolean state |
| useWindowSize | Window size |

## Quick Component Selection Guide

### For Forms

- Simple input: **Field**
- Date selection: **Calendar** or **DatePicker**
- Time selection: **TimePicker**
- Multiple choice: **Checkbox**
- Single choice: **Radio**
- Rating: **Rate**
- File upload: **Uploader**
- Search: **Search**

### For Navigation

- Top navigation: **NavBar**
- Bottom tabs: **Tabbar**
- Side navigation: **Sidebar**
- Tab content: **Tab**
- Back to top: **BackTop**

### For Feedback

- Toast message: **Toast**
- Modal dialog: **Dialog**
- Notification: **Notify**
- Loading state: **Loading**

### For Display

- List items: **Cell**
- Progress: **Progress** or **Circle**
- Empty state: **Empty**
- Tags: **Tag**
- Badges: **Badge**

### For Actions

- Action selection: **ActionSheet**
- Share: **ShareSheet**
- Dropdown: **DropdownMenu**
- Swipe actions: **SwipeCell**

## Common Props Patterns

### Size Props

Most components support size props:
- `large` - Large size
- `normal` - Default size
- `small` - Small size
- `mini` - Mini size

### Type Props

Common type values:
- `primary` - Primary action
- `success` - Success state
- `warning` - Warning state
- `danger` - Danger/error state
- `default` - Default style

### Shape Props

- `round` - Rounded corners
- `square` - Square shape
- `plain` - Plain/outline style

### State Props

- `disabled` - Disabled state
- `loading` - Loading state
- `readonly` - Read-only state

## Best Practices

1. **Choose the right component**: Select components based on use case, not visual similarity.

2. **Use composables**: Leverage Vue 3 composables for reusable logic.

3. **Combine components**: Many components work well together (e.g., Form + Field).

4. **Check component docs**: Each component has specific props and events.

5. **Use TypeScript**: Import types for better development experience.

## Input Parameters

When using this skill, provide the following information:
- **Use case**: What functionality is needed
- **Category**: Which component category to focus on
- **Features**: Specific features required (e.g., validation, lazy loading)

## Output Format

This skill provides:
1. Component category overview
2. Component recommendations based on use case
3. Common props and patterns
4. Related component suggestions
5. Links to detailed component documentation

## Usage Limitations

- This is an overview skill; for detailed component usage, refer to specific component documentation
- Component availability may vary by Vant version
- Some components require additional configuration
