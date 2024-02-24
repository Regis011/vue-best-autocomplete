# Vue Autocomplete Component

A Vue.js component for autocomplete functionality in input fields.

## Installation

You can install the package via npm:
Copy code

```
npm install vue-autocomplete-component
```

## Usage

Basic Usage
Copy code

```
<template>
  <autocomplete :items="addressList" @selected="handleSelected"></autocomplete>
</template>

<script>
import Autocomplete from 'vue-autocomplete-component';

export default {
  components: {
    Autocomplete,
  },
  data() {
    return {
      addressList: [
        { id: 1, title: 'New York, USA' },
        { id: 2, title: 'London, UK' },
        // Add more address objects as needed
      ],
    };
  },
  methods: {
    handleSelected(address) {
      console.log('Selected address:', address);
      // Handle selected address
    },
  },
};
</script>
```

### Props

- `items` (Array): An array of objects representing the autocomplete options. Each object should have at least an id and title property.

### Events

- `selected`: Triggered when an option is selected. Emits the selected option object.

### Customization

You can customize the appearance of the autocomplete input and suggestions by overriding the CSS classes provided by the component.

### CSS Classes

- `.input-wrapper`: Wrapper class for the input field.
- `.data-input-success`: Class applied when input is successful.
- `.base-input-error`: Class applied when there's an error in input.
- `.suggestion-list-active`: Class applied to the suggestion list when active.

#### Example

You can customize the appearance by overriding these CSS classes in your project's stylesheet.

## License

This project is licensed under the GNU License - see the [LICENSE](https://github.com/Regis011/vue-best-autocomplete/blob/main/LICENSE) file for details.
