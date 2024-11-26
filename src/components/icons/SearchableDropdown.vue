<template>
  <div class="dropdown" v-if="options">
    <!-- Dropdown Input with Search Icon -->
    <div class="input-wrapper">
      <span class="search-icon">🔍<i class="i-carbon-search"></i></span> <!-- You can replace this with an SVG or FontAwesome icon -->
      <input
        class="dropdown-input"
        :name="name"
        @focus="showOptions()"
        @blur="exit()"
        @keyup="keyMonitor"
        v-model="searchFilter"
        :disabled="disabled"
        :placeholder="placeholder"
      />
    </div>

    <!-- Dropdown Menu -->
    <div class="dropdown-content" v-show="optionsShown">
      <div
        class="dropdown-item"
        @mousedown="selectOption(option)"
        v-for="(option, index) in filteredOptions"
        :key="index">
        {{ option.name || option.id || '-' }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Dropdown',
  props: {
    name: {
      type: String,
      required: false,
      default: 'dropdown',
    },
    options: {
      type: Array,
      required: true,
      default: () => [],
    },
    placeholder: {
      type: String,
      required: false,
      default: 'Select account',
    },
    disabled: {
      type: Boolean,
      required: false,
      default: false,
    },
    maxItem: {
      type: Number,
      required: false,
      default: 6,
    }
  },
  data() {
    return {
      selected: {},
      optionsShown: false,
      searchFilter: ''
    }
  },
  created() {
    this.$emit('selected', this.selected);
  },
  computed: {
    filteredOptions() {
      const filtered = [];
      const regOption = new RegExp(this.searchFilter, 'ig');
      for (const option of this.options) {
        if (this.searchFilter.length < 1 || option.name.match(regOption)){
          if (filtered.length < this.maxItem) filtered.push(option);
        }
      }
      return filtered;
    }
  },
  methods: {
    selectOption(option) {
      this.selected = option;
      this.optionsShown = false;
      this.searchFilter = this.selected.name;
      this.$emit('selected', this.selected);
    },
    showOptions(){
      if (!this.disabled) {
        this.searchFilter = '';
        this.optionsShown = true;
      }
    },
    exit() {
      if (!this.selected.id) {
        this.selected = {};
        this.searchFilter = '';
      } else {
        this.searchFilter = this.selected.name;
      }
      this.$emit('selected', this.selected);
      this.optionsShown = false;
    },
    keyMonitor(event) {
      if (event.key === "Enter" && this.filteredOptions[0])
        this.selectOption(this.filteredOptions[0]);
    }
  },
  watch: {
    searchFilter() {
      if (this.filteredOptions.length === 0) {
        this.selected = {};
      } else {
        this.selected = this.filteredOptions[0];
      }
      this.$emit('filter', this.searchFilter);
    }
  }
};
</script>

<style scoped>
.dropdown {
  position: relative;
  display: block;
  margin: 0.2em auto;
  width: 75%;

  .input-wrapper {
    position: relative; /* Position relative to allow absolute positioning of the icon */

    .search-icon {
      position: absolute;
      left: 20px;
      top: 50%;
      transform: translateY(-50%);
      pointer-events: none;
    }

    .dropdown-input {
      background: #fff;
      cursor: pointer;
      border: 1px solid #e7ecf5;
      color: #333;
      display: block;
      font-size: 1.1em;
      padding: 6px 6px 6px 50px;

      height: 50px;
      border-radius: 10px;
      width: 100%;


      min-width: 250px;
      /*max-width: 250px;*/

      &:hover {
        background: #f8f8fa;
        border-color: aqua;
      }

      &::selection {
        border-color: chartreuse;
      }
    }
  }

  .dropdown-content {
    position: absolute;
    background-color: #fff;
    margin-left: 5px;
    width: calc(100% - 10px);
    border: 1px solid #e7ecf5;
    box-shadow: 0px -8px 34px rgba(0,0,0,0.05);
    overflow-y: auto; /* Allow vertical scrolling */
    z-index: 1;

    .dropdown-item {
      color: black;
      font-size:1em;

      line-height:.9em;
      padding:.5em;
      margin-top: .3em;
      text-decoration:none;
      display:block;

      cursor:pointer;

      &:hover {
        background-color:#e7ecf5;
      }
    }
  }

  .dropdown:hover .dropdown-content {
    display:block;
  }
}
</style>
