# Local Development Guide

## Quick Start

To test the autocomplete component locally:

```bash
# Install dependencies
npm install --legacy-peer-deps

# Start the development server
npm run dev
```

The app will be available at **http://localhost:8080**

## What You'll See

The demo app includes three interactive examples:

1. **City Search** - Real-time filtering with success state
2. **Country Search** - With validation and error state
3. **Programming Languages** - Simple selection example

## Features to Test

- ✅ Type to filter suggestions
- ✅ Click to select
- ✅ Keyboard navigation (Arrow Up/Down)
- ✅ Press Enter to select
- ✅ Press Esc to close
- ✅ Visual feedback (success/error states)

## Development Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Start dev server with hot-reload |
| `npm run build` | Build demo app for production |
| `npm run build:lib` | Build component as npm library |
| `npm run lint` | Run ESLint |

## Modifying the Demo

Edit `src/App.vue` to:
- Add more examples
- Change sample data
- Test different configurations
- Customize styling

## Component API

### Props
- `items` - Array of objects with `{id, title}` structure
- `handleStyleState` - Object for visual states: `{success, noSearchError, chosenAddress}`

### Events
- `@change` - Fires on input change (emits query string)
- `@selected` - Fires when item selected (emits selected object)

## Example Usage

```vue
<template>
  <Autocomplete
    :items="myItems"
    :handleStyleState="state"
    @change="handleChange"
    @selected="handleSelected"
  />
</template>

<script>
import Autocomplete from './components/autocomplete/input.vue'

export default {
  components: { Autocomplete },
  data () {
    return {
      myItems: [
        { id: 1, title: 'Option 1' },
        { id: 2, title: 'Option 2' }
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
      // Handle input change
    },
    handleSelected (item) {
      // Handle selection
      this.state.success = true
      this.state.chosenAddress = item.title
    }
  }
}
</script>
```

## Building for NPM

When ready to publish:

```bash
npm run build:lib
npm run publish:lib
```

This creates the distributable component in the `dist/` folder.
