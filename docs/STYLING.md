# Styling Guide

Guide for customizing the appearance of the Vue Best Autocomplete component.

## Default Styles

The component comes with pre-built styles that include:

- Modern rounded input field
- Dropdown with smooth transitions
- Success and error state indicators
- Keyboard navigation highlighting
- Responsive design

## Including Styles

```javascript
import 'vue-best-autocomplete/dist/Autocomplete.css'
```

## Component Structure

```html
<div class="input-wrapper">
  <input id="input-autocomplete" />
  <ul role="listbox">
    <li class="active-option">Option 1</li>
    <li>Option 2</li>
  </ul>
</div>
```

## CSS Classes Reference

### Main Wrapper

```css
.input-wrapper {
  position: relative;
}
```

**State Modifiers:**
- `.data-input-success` - Applied when selection is successful
- `.base-input-error` - Applied when there's an error
- `.suggestion-list-active` - Applied when suggestions are visible

### Input Element

```css
.input-wrapper input {
  border: none;
  border-radius: 12px;
  box-shadow: 0 3px 18px rgba(42, 42, 43, 0.12);
  font-size: 1.8rem;
  font-weight: 420;
  height: 60px;
  padding: 1.5rem 1.8rem;
  width: 100%;
}
```

### Suggestions List

```css
.input-wrapper ul {
  position: absolute;
  background-color: white;
  list-style-type: none;
  border-bottom-right-radius: 24px;
  border-bottom-left-radius: 24px;
}
```

### List Items

```css
.input-wrapper ul li {
  padding: 9px 18px;
  cursor: pointer;
}

.input-wrapper ul li:hover,
.input-wrapper ul li.active-option {
  background-color: #aec6cf;
}
```

## Customization Examples

### Example 1: Change Input Height and Font Size

```css
.input-wrapper input {
  height: 50px;
  font-size: 16px;
  padding: 12px 16px;
}
```

### Example 2: Custom Colors

```css
/* Primary color theme */
.input-wrapper ul li:hover,
.input-wrapper ul li.active-option {
  background-color: #007bff;
  color: white;
}

/* Success state */
.input-wrapper.data-input-success > input {
  border-bottom: 3px solid #28a745;
}

/* Error state */
.input-wrapper.base-input-error {
  border-bottom: 3px solid #dc3545;
}
```

### Example 3: Material Design Style

```css
.input-wrapper input {
  border: none;
  border-bottom: 2px solid #e0e0e0;
  border-radius: 0;
  box-shadow: none;
  font-size: 16px;
  height: 48px;
  padding: 12px 0;
  transition: border-color 0.2s;
}

.input-wrapper input:focus {
  border-bottom-color: #1976d2;
}

.input-wrapper ul {
  border-radius: 4px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
  margin-top: 4px;
}

.input-wrapper ul li.active-option {
  background-color: #e3f2fd;
  color: #1976d2;
}
```

### Example 4: Dark Mode

```css
.input-wrapper input {
  background-color: #2d2d2d;
  color: #ffffff;
  border-color: #404040;
}

.input-wrapper ul {
  background-color: #2d2d2d;
  color: #ffffff;
}

.input-wrapper ul li:hover,
.input-wrapper ul li.active-option {
  background-color: #404040;
}
```

### Example 5: Custom Border Styles

```css
.input-wrapper input {
  border: 2px solid #ddd;
  border-radius: 8px;
  box-shadow: none;
}

.input-wrapper.suggestion-list-active > input {
  border-bottom-left-radius: 0;
  border-bottom-right-radius: 0;
  border-bottom-color: #007bff;
}

.input-wrapper ul {
  border: 2px solid #007bff;
  border-top: none;
  border-bottom-left-radius: 8px;
  border-bottom-right-radius: 8px;
}
```

### Example 6: Compact Size

```css
.input-wrapper input {
  height: 40px;
  font-size: 14px;
  padding: 8px 12px;
  border-radius: 6px;
}

.input-wrapper ul {
  border-radius: 6px;
  font-size: 14px;
}

.input-wrapper ul li {
  padding: 6px 12px;
}
```

### Example 7: Remove Success/Error Icons

The success and error icons are added using CSS `::after` pseudo-elements with base64 SVG data. To remove them:

```css
.input-wrapper.data-input-success::after,
.input-wrapper.base-input-error::after {
  display: none;
}
```

Or customize them:

```css
.input-wrapper.data-input-success::after {
  content: '✓';
  position: absolute;
  right: 12px;
  top: 50%;
  transform: translateY(-50%);
  color: #28a745;
  font-size: 24px;
}
```

## Scoped Styles

If you want to customize only specific instances, use wrapper classes:

```vue
<template>
  <div class="my-custom-autocomplete">
    <Autocomplete :items="items" />
  </div>
</template>

<style scoped>
.my-custom-autocomplete .input-wrapper input {
  background-color: #f5f5f5;
  border: 1px solid #ccc;
}

.my-custom-autocomplete .input-wrapper ul li.active-option {
  background-color: #ffeb3b;
  color: #000;
}
</style>
```

## Using CSS Variables

For easier theming, you can define CSS variables:

```css
:root {
  --autocomplete-border-radius: 12px;
  --autocomplete-input-height: 60px;
  --autocomplete-font-size: 18px;
  --autocomplete-primary-color: #007bff;
  --autocomplete-success-color: #28a745;
  --autocomplete-error-color: #dc3545;
}

.input-wrapper input {
  border-radius: var(--autocomplete-border-radius);
  height: var(--autocomplete-input-height);
  font-size: var(--autocomplete-font-size);
}

.input-wrapper ul li.active-option {
  background-color: var(--autocomplete-primary-color);
  color: white;
}

.input-wrapper.data-input-success > input {
  border-bottom-color: var(--autocomplete-success-color);
}

.input-wrapper.base-input-error {
  border-bottom-color: var(--autocomplete-error-color);
}
```

## Important Notes

1. **Font Size Units**: The default styles use `rem` units. If you need different sizing, ensure your root font size is set appropriately or use `px` units.

2. **Specificity**: If your custom styles aren't applying, you may need to increase specificity:
   ```css
   /* More specific selector */
   div.input-wrapper input#input-autocomplete {
     /* your styles */
   }
   ```

3. **z-index**: The suggestions dropdown uses `z-index: 10`. Adjust if needed:
   ```css
   .input-wrapper ul {
     z-index: 1000;
   }
   ```

4. **Transitions**: Add smooth transitions for better UX:
   ```css
   .input-wrapper ul li {
     transition: background-color 0.2s ease, color 0.2s ease;
   }
   ```
