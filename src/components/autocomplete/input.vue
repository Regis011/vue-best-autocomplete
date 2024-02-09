<template>
  <div class="input-wrapper" :class="handleInputState">
    <input
      v-model="query"
      @input="updateQuery"
      @focus="showSuggestions"
      @keydown.down="handleDown"
      @keydown.up="handleUp"
      @keydown.esc="hideSuggestions"
      @keydown.enter="handleEnter"
      aria-haspopup="true"
      role="combobox"
      aria-expanded="true"
      :aria-activedescendant="query"
      placeholder="Skriv din adress här"
      id="input-autocomplete"
    />
    <ul v-if="showResults" role="listbox">
      <li
        v-for="(result, index) in results"
        :key="result.id"
        @click="handleClick(result)"
        @keydown.enter="selectResult(result)"
        role="option"
        tabindex="-1"
        :aria-selected="isActive(index)"
        :id="getResultId(index)"
        :class="{ 'active-option': isActive(index) }"
      >
        {{ result.title }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    items: {
      type: Array,
      default: () => []
    },
    handleStyleState: {
      type: Object,
      default: () => ({
        success: false,
        noSearchError: false,
        chosenAddress: ''
      })
    }
  },

  data () {
    return {
      query: '',
      showResults: false,
      results: [],
      activeIndex: 0
    }
  },

  computed: {
    handleInputState () {
      return {
        'data-input-success':
          this.handleStyleState.success && this.handleStyleState.chosenAddress,
        'suggestion-list-active': this.results.length > 0 && this.showResults,
        'base-input-error':
          this.handleStyleState.noSearchError &&
          !this.handleStyleState.chosenAddress
      }
    }
  },

  methods: {
    updateQuery () {
      this.results = this.items.filter(address =>
        address.title.toLowerCase().includes(this.query.toLowerCase())
      )
      this.showResults = !!this.query
      this.$emit('change', this.query)
    },

    showSuggestions () {
      this.showResults = true
    },

    hideSuggestions () {
      this.showResults = false
    },

    selectResult (result) {
      this.query = result.title
      this.$emit('selected', result)
      this.showResults = false
      this.activeIndex = -1
    },

    handleEnter () {
      if (this.results.length > 0) {
        this.selectResult(this.results[this.activeIndex])
      }
    },

    handleDown () {
      if (this.activeIndex < this.results.length - 1) {
        this.activeIndex++
      } else {
        this.activeIndex = 0
      }
    },

    handleUp () {
      if (this.activeIndex > 0) {
        this.activeIndex--
      } else {
        this.activeIndex = this.results.length - 1
      }
    },

    isActive (index) {
      return index === this.activeIndex
    },

    getResultId (index) {
      return `result-${index}`
    },

    handleClick (result) {
      this.selectResult(result)
      this.$nextTick(() => {
        this.hideSuggestions()
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.input-wrapper {
  position: relative;

  input {
    position: relative;
    border: none;
    border-radius: 12px;
    box-shadow: 0 3px 18px rgba(42, 42, 43, 0.12);
    font-size: 1.8rem;
    font-weight: 420;
    height: 60px;
    padding: 1.5rem 1.8rem;
    width: 100%;
    &:focus {
      outline: none;
    }
  }

  &.data-input-success {
    > input {
      border-bottom: 3px solid var(--green);
      position: relative;
    }
    &::after {
      content: url('data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPGNpcmNsZSBjeD0iMTIiIGN5PSIxMiIgcj0iMTEiIGZpbGw9IiM1OUNDOUUiLz4KPHBhdGggZD0iTTE2LjY2NjYgOC41TDEwLjI0OTkgMTQuOTE2N0w3LjMzMzI1IDEyIiBzdHJva2U9IndoaXRlIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1saW5lY2FwPSJyb3VuZCIgc3Ryb2tlLWxpbmVqb2luPSJyb3VuZCIvPgo8L3N2Zz4K');
      position: absolute;
      right: 12px;
      top: 18px;
    }
  }

  &.base-input-error {
    border-radius: 12px;
    border-bottom: 3px solid var(--red);
    background-color: var(--white);
    &::after {
      content: url('data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPGNpcmNsZSBjeD0iMTIiIGN5PSIxMiIgcj0iMTEiIGZpbGw9IiNGRDU0NTciLz4KPHBhdGggZD0iTTEyIDYuNzVWMTMuNSIgc3Ryb2tlPSJ3aGl0ZSIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbGluZWNhcD0icm91bmQiIHN0cm9rZS1saW5lam9pbj0iYmV2ZWwiLz4KPGNpcmNsZSBjeD0iMTIiIGN5PSIxNi44NzUiIHI9IjEuMTI1IiBmaWxsPSJ3aGl0ZSIvPgo8L3N2Zz4K');
      position: absolute;
      right: 12px;
      top: 18px;
    }
  }

  &.suggestion-list-active {
    > input {
      border-bottom-left-radius: 0;
      border-bottom-right-radius: 0;
      border-bottom: 2px solid var(--black);
    }
  }

  ul {
    position: absolute;
    left: 0;
    right: 0;
    top: 100%;
    background-color: var(--white);
    opacity: 1;
    z-index: 10;
    list-style-type: none;
    margin: 0;
    padding: 0;
    @include font(3, 'medium');

    border-bottom-right-radius: 24px;
    border-bottom-left-radius: 24px;
    //box-shadow: 0 3px 18px rgba(42, 42, 43, 12%);
    li {
      padding: 9px 18px;
      text-align: left;
      cursor: pointer;
      transition: background-color 0.2s, outline 0.2s;
      &:hover,
      &:focus,
      &.active-option {
        background-color: var(--light-blue);
      }
    }
  }
}
</style>
