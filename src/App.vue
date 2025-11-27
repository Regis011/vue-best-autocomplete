<template>
  <div id="app">
    <div class="container">
      <h1>Vue Best Autocomplete - Demo</h1>

      <div class="demo-section">
        <h2>Example 1: City Search</h2>
        <p>Start typing to search for cities...</p>
        <Autocomplete
          :items="cities"
          :handleStyleState="cityState"
          @change="handleCityChange"
          @selected="handleCitySelected"
        />
        <div v-if="selectedCity" class="result">
          <strong>Selected:</strong> {{ selectedCity.title }}
        </div>
      </div>

      <div class="demo-section">
        <h2>Example 2: Country Search with Validation</h2>
        <p>Search for a country (shows error if empty on blur)...</p>
        <Autocomplete
          :items="countries"
          :handleStyleState="countryState"
          @change="handleCountryChange"
          @selected="handleCountrySelected"
        />
        <div v-if="selectedCountry" class="result">
          <strong>Selected:</strong> {{ selectedCountry.title }}
        </div>
      </div>

      <div class="demo-section">
        <h2>Example 3: Programming Languages</h2>
        <p>Select your favorite programming language...</p>
        <Autocomplete
          :items="languages"
          :handleStyleState="languageState"
          @change="handleLanguageChange"
          @selected="handleLanguageSelected"
        />
        <div v-if="selectedLanguage" class="result">
          <strong>Selected:</strong> {{ selectedLanguage.title }}
        </div>
      </div>

      <div class="info-section">
        <h3>Component Features:</h3>
        <ul>
          <li>✅ Real-time filtering as you type</li>
          <li>✅ Keyboard navigation (Arrow Up/Down, Enter, Esc)</li>
          <li>✅ Visual states (success, error)</li>
          <li>✅ Click and keyboard selection</li>
          <li>✅ Accessible with ARIA attributes</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import Autocomplete from './components/autocomplete/input.vue'

export default {
  name: 'App',
  components: {
    Autocomplete
  },
  data () {
    return {
      // Cities data
      cities: [
        { id: 1, title: 'New York' },
        { id: 2, title: 'London' },
        { id: 3, title: 'Paris' },
        { id: 4, title: 'Tokyo' },
        { id: 5, title: 'Berlin' },
        { id: 6, title: 'Sydney' },
        { id: 7, title: 'Toronto' },
        { id: 8, title: 'Dubai' },
        { id: 9, title: 'Singapore' },
        { id: 10, title: 'Barcelona' },
        { id: 11, title: 'Amsterdam' },
        { id: 12, title: 'Stockholm' },
        { id: 13, title: 'Copenhagen' },
        { id: 14, title: 'Vienna' },
        { id: 15, title: 'Prague' }
      ],
      selectedCity: null,
      cityState: {
        success: false,
        noSearchError: false,
        chosenAddress: ''
      },

      // Countries data
      countries: [
        { id: 1, title: 'United States' },
        { id: 2, title: 'United Kingdom' },
        { id: 3, title: 'France' },
        { id: 4, title: 'Germany' },
        { id: 5, title: 'Japan' },
        { id: 6, title: 'Australia' },
        { id: 7, title: 'Canada' },
        { id: 8, title: 'Spain' },
        { id: 9, title: 'Italy' },
        { id: 10, title: 'Netherlands' },
        { id: 11, title: 'Sweden' },
        { id: 12, title: 'Norway' },
        { id: 13, title: 'Denmark' },
        { id: 14, title: 'Switzerland' },
        { id: 15, title: 'Austria' }
      ],
      selectedCountry: null,
      countryState: {
        success: false,
        noSearchError: false,
        chosenAddress: ''
      },

      // Programming languages
      languages: [
        { id: 1, title: 'JavaScript' },
        { id: 2, title: 'Python' },
        { id: 3, title: 'Java' },
        { id: 4, title: 'TypeScript' },
        { id: 5, title: 'C++' },
        { id: 6, title: 'C#' },
        { id: 7, title: 'Ruby' },
        { id: 8, title: 'Go' },
        { id: 9, title: 'Rust' },
        { id: 10, title: 'PHP' },
        { id: 11, title: 'Swift' },
        { id: 12, title: 'Kotlin' },
        { id: 13, title: 'Vue.js' },
        { id: 14, title: 'React' },
        { id: 15, title: 'Angular' }
      ],
      selectedLanguage: null,
      languageState: {
        success: false,
        noSearchError: false,
        chosenAddress: ''
      }
    }
  },
  methods: {
    // City handlers
    handleCityChange (query) {
      this.cityState.success = false
      this.cityState.chosenAddress = ''
    },
    handleCitySelected (city) {
      this.selectedCity = city
      this.cityState.success = true
      this.cityState.chosenAddress = city.title
    },

    // Country handlers
    handleCountryChange (query) {
      this.countryState.success = false
      this.countryState.chosenAddress = ''
      if (!query) {
        this.countryState.noSearchError = true
      } else {
        this.countryState.noSearchError = false
      }
    },
    handleCountrySelected (country) {
      this.selectedCountry = country
      this.countryState.success = true
      this.countryState.chosenAddress = country.title
      this.countryState.noSearchError = false
    },

    // Language handlers
    handleLanguageChange (query) {
      this.languageState.success = false
      this.languageState.chosenAddress = ''
    },
    handleLanguageSelected (language) {
      this.selectedLanguage = language
      this.languageState.success = true
      this.languageState.chosenAddress = language.title
    }
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}

html {
  font-size: 62.5%; /* 1rem = 10px */
}

body {
  margin: 0;
  padding: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  min-height: 100vh;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  padding: 2rem;
}

.container {
  max-width: 800px;
  margin: 0 auto;
  background: white;
  border-radius: 16px;
  padding: 3rem;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.2);
}

h1 {
  font-size: 3.2rem;
  margin-top: 0;
  margin-bottom: 3rem;
  color: #667eea;
  text-align: center;
}

h2 {
  font-size: 2.2rem;
  margin-bottom: 1rem;
  color: #333;
}

h3 {
  font-size: 2rem;
  color: #555;
  margin-bottom: 1.5rem;
}

p {
  font-size: 1.6rem;
  color: #666;
  margin-bottom: 1.5rem;
}

.demo-section {
  margin-bottom: 4rem;
  padding-bottom: 3rem;
  border-bottom: 2px solid #f0f0f0;
}

.demo-section:last-of-type {
  border-bottom: none;
}

.result {
  margin-top: 1.5rem;
  padding: 1.5rem;
  background-color: #f8f9fa;
  border-radius: 8px;
  font-size: 1.6rem;
  color: #333;
}

.info-section {
  background-color: #f0f4ff;
  padding: 2rem;
  border-radius: 12px;
  margin-top: 3rem;
}

.info-section ul {
  list-style: none;
  padding: 0;
  margin: 0;
  font-size: 1.6rem;
}

.info-section li {
  padding: 0.8rem 0;
  color: #555;
}
</style>
