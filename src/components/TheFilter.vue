<script>
import { ref } from 'vue'
import SearchIcon from '../assests/search-icon.vue'
import Toggle from './ButtonSearchToggle.vue'
import TheAdvancedFilter from './TheAdvancedFilter.vue'
export default {
  components: { TheAdvancedFilter, Toggle, SearchIcon },

  name: 'Filter',
  emits: ['searchInput'],

  setup() {
    let advancedSearch = ref(false)
    return { advancedSearch }
  },

  data() {
    return {
      searchInput: ''
    }
  },
  mounted() {
    let input = document.getElementById('searchInput')

    input.addEventListener('keypress', (event) => {
      if (event.key === 'Enter') {
        event.preventDefault()
        this.sendSearchInput()
      }
    })
  },

  methods: {
    sendSearchInput() {
      this.$emit('search-input', this.searchInput)
    },

    handleFormData(data) {
      const formDataFiltered = Object.fromEntries(
        Object.entries(data).filter(([key, value]) => value !== '')
      )
      this.searchInput = formDataFiltered
      this.sendSearchInput()
    },

    setAdvancedSearch() {
      this.advancedSearch = !this.advancedSearch
    }
  }
}
</script>

<template>
  <div>
    <div class="py-3 pl-2">
      <Toggle @is-active="setAdvancedSearch" />
    </div>
    <div v-if="!advancedSearch">
      <div class="flex justify-between py-3 pl-2">
        <div class="relative max-w-xs flex">
          <label for="searchInput" class="sr-only"> Search </label>
          <input
            id="searchInput"
            type="text"
            v-model="searchInput"
            name="searchInput"
            class="block w-full p-3 text-sm border-gray-200 rounded-md focus:border-blue-500 focus:ring-blue-500 dark:bg-gray-100 dark:border-gray-700 dark:text-gray-800"
            placeholder="Search..."
          />
          <div>
            <button
              @click="sendSearchInput"
              class="block max-w-xs ml-2 p-3 border-gray-200 rounded-md dark:bg-gray-100 hover:bg-gray-300"
            >
              <SearchIcon />
            </button>
          </div>
        </div>
      </div>
    </div>
    <div v-else>
      <TheAdvancedFilter @form-data="handleFormData" />
    </div>
  </div>
</template>
