# Vue Best Autocomplete

A simple and flexible Vue 3 autocomplete component with keyboard navigation, visual states, and accessibility features.

## Features

✨ Real-time filtering as you type  
⌨️ Keyboard navigation (Arrow keys, Enter, Escape)  
🎨 Visual states (success, error)  
♿ Accessible with ARIA attributes  
🎯 Easy to customize  

## Installation

```bash
npm install vue-best-autocomplete
```

## Usage

### Basic Example

```vue
<template>
  <Autocomplete
    :items="items"
    :handleStyleState="state"
    @change="handleChange"
    @selected="handleSelected"
  />
</template>

<script>
import Autocomplete from 'vue-best-autocomplete'
import 'vue-best-autocomplete/dist/Autocomplete.css'

export default {
  components: {
    Autocomplete
  },
  data () {
    return {
      items: [
        { id: 1, title: 'New York, USA' },
        { id: 2, title: 'London, UK' },
        { id: 3, title: 'Paris, France' },
        // Add more items as needed
      ],
      state: {
        success: false,
        noSearchError: false,
        chosenAddress: ''
      }
    }
  },
  methods: {
    handleChange (query) {
      // Reset state on input change
      this.state.success = false
      this.state.chosenAddress = ''
    },
    handleSelected (item) {
      console.log('Selected:', item)
      // Update state to show success
      this.state.success = true
      this.state.chosenAddress = item.title
    }
  }
}
</script>
```

## API

### Props

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `items` | Array | Yes | `[]` | Array of objects with `id` and `title` properties |
| `handleStyleState` | Object | No | `{}` | Object controlling visual states (see below) |

#### handleStyleState Object

```javascript
{
  success: false,        // Shows success indicator (green border + checkmark)
  noSearchError: false,  // Shows error indicator (red border + error icon)
  chosenAddress: ''      // The selected value (used for success state)
}
```

### Events

| Event | Payload | Description |
|-------|---------|-------------|
| `@change` | `String` | Emitted when input value changes. Returns the current query string |
| `@selected` | `Object` | Emitted when an item is selected. Returns the selected item object |

## Customization

### CSS Classes

You can customize the appearance by overriding these CSS classes:

| Class | Description |
|-------|-------------|
| `.input-wrapper` | Main wrapper for the input and suggestions |
| `.data-input-success` | Applied when input is in success state |
| `.base-input-error` | Applied when input has an error |
| `.suggestion-list-active` | Applied when suggestions are visible |
| `.active-option` | Applied to the currently highlighted option |

### Example Customization

```css
/* Override input styles */
.input-wrapper input {
  border-radius: 8px;
  font-size: 16px;
}

/* Customize suggestion list */
.input-wrapper ul {
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

/* Customize active option */
.input-wrapper li.active-option {
  background-color: #4CAF50;
  color: white;
}
```

## Keyboard Navigation

- **Arrow Down** - Move to next option
- **Arrow Up** - Move to previous option
- **Enter** - Select highlighted option
- **Escape** - Close suggestions

## Contributing

Contributions are welcome! See [docs/DEVELOPMENT.md](./docs/DEVELOPMENT.md) for local development setup.

## License

This project is licensed under the MIT License - see the [LICENSE](https://github.com/Regis011/vue-best-autocomplete/blob/main/LICENSE) file for details.
