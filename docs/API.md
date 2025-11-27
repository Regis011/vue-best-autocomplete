# API Reference

Complete API documentation for the Vue Best Autocomplete component.

## Component Props

### items

- **Type:** `Array`
- **Required:** Yes
- **Default:** `[]`

Array of objects representing autocomplete options. Each object must have the following structure:

```javascript
{
  id: Number | String,  // Unique identifier
  title: String         // Display text
}
```

**Example:**

```javascript
items: [
  { id: 1, title: 'New York, USA' },
  { id: 2, title: 'London, UK' },
  { id: 3, title: 'Paris, France' }
]
```

### handleStyleState

- **Type:** `Object`
- **Required:** No
- **Default:** `{ success: false, noSearchError: false, chosenAddress: '' }`

Object controlling the visual state of the input field.

**Properties:**

| Property | Type | Description |
|----------|------|-------------|
| `success` | Boolean | When `true`, displays success state (green border + checkmark icon) |
| `noSearchError` | Boolean | When `true`, displays error state (red border + error icon) |
| `chosenAddress` | String | The selected value - used in combination with `success` to display success state |

**Example:**

```javascript
handleStyleState: {
  success: true,
  noSearchError: false,
  chosenAddress: 'New York, USA'
}
```

## Events

### @change

Emitted when the input value changes (on every keystroke).

**Payload:** `String` - The current query/search text

**Example:**

```vue
<Autocomplete
  :items="items"
  @change="handleChange"
/>

<script>
export default {
  methods: {
    handleChange (query) {
      console.log('User typed:', query)
      // Reset validation state, fetch new data, etc.
    }
  }
}
</script>
```

### @selected

Emitted when a user selects an item from the suggestions list.

**Payload:** `Object` - The complete selected item object from the `items` array

**Example:**

```vue
<Autocomplete
  :items="items"
  @selected="handleSelected"
/>

<script>
export default {
  methods: {
    handleSelected (item) {
      console.log('Selected item:', item)
      // { id: 1, title: 'New York, USA' }
      
      // Update state, navigate, save to database, etc.
    }
  }
}
</script>
```

## Component Behavior

### Filtering

The component automatically filters the `items` array based on user input using case-insensitive string matching:

```javascript
items.filter(item =>
  item.title.toLowerCase().includes(query.toLowerCase())
)
```

### Keyboard Navigation

The component supports full keyboard navigation:

| Key | Action |
|-----|--------|
| `↓` (Arrow Down) | Move selection to next item (loops to first if at end) |
| `↑` (Arrow Up) | Move selection to previous item (loops to last if at start) |
| `Enter` | Select the currently highlighted item |
| `Esc` | Close the suggestions dropdown |

### Accessibility

The component includes ARIA attributes for screen reader support:

- `role="combobox"` on input
- `aria-haspopup="true"`
- `aria-expanded="true"`
- `role="listbox"` on suggestions list
- `role="option"` on each suggestion
- `aria-selected` on active option

## CSS Classes

### Component States

| Class | When Applied | Description |
|-------|--------------|-------------|
| `.input-wrapper` | Always | Main wrapper element |
| `.data-input-success` | `handleStyleState.success === true` | Success state styling |
| `.base-input-error` | `handleStyleState.noSearchError === true` | Error state styling |
| `.suggestion-list-active` | Suggestions visible | Applied when dropdown is open |

### List Items

| Class | When Applied | Description |
|-------|--------------|-------------|
| `.active-option` | Item is highlighted | Applied to the currently selected option in the list |

## Visual States

### Success State

Shows a green checkmark icon and green bottom border.

**Trigger:**
```javascript
handleStyleState: {
  success: true,
  chosenAddress: 'Some Value'
}
```

### Error State

Shows a red error icon and red bottom border.

**Trigger:**
```javascript
handleStyleState: {
  noSearchError: true
}
```

### Active Dropdown

Shows suggestions list with styled border radius and no bottom border on input.

**Trigger:** User types in the input (automatic)

## Complete Usage Example

```vue
<template>
  <div>
    <h2>Select a City</h2>
    <Autocomplete
      :items="cities"
      :handleStyleState="cityState"
      @change="onCityChange"
      @selected="onCitySelected"
    />
    <p v-if="selectedCity">You selected: {{ selectedCity.title }}</p>
  </div>
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
      cities: [
        { id: 1, title: 'New York' },
        { id: 2, title: 'London' },
        { id: 3, title: 'Paris' },
        { id: 4, title: 'Tokyo' }
      ],
      selectedCity: null,
      cityState: {
        success: false,
        noSearchError: false,
        chosenAddress: ''
      }
    }
  },
  methods: {
    onCityChange (query) {
      // Reset state when user types
      this.cityState.success = false
      this.cityState.chosenAddress = ''
      
      // Show error if empty (optional)
      if (!query) {
        this.cityState.noSearchError = true
      } else {
        this.cityState.noSearchError = false
      }
    },
    onCitySelected (city) {
      // Save selection
      this.selectedCity = city
      
      // Update state to show success
      this.cityState.success = true
      this.cityState.chosenAddress = city.title
      this.cityState.noSearchError = false
    }
  }
}
</script>
```
