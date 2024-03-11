<script>
export default {
  data() {
    return {
      isActive: false
    }
  },
  methods: {
    toggleIsActive() {
      this.isActive = !this.isActive
      this.$emit('is-active', this.isActive)
    }
  }
}
</script>

<template>
  <div class="flex items-center space-x-2">
    <div class="relative">
      <button
        @click="toggleIsActive"
        class="relative z-0 inline-flex text-sm rounded-md shadow-sm focus:ring-accent-500 focus:border-accent-500 bg-slate-300 hover:bg-gray-200 focus:z-10 focus:outline-none focus:ring-1 transition-colors duration-300"
        style="transition: background-color 0.3s, opacity 0.3s"
      >
        <span
          class="relative inline-flex items-center px-3 py-3 space-x-2 text-sm font-medium text-gray-600 bg-opacity-100 bg-slate-300 hover:bg-opacity-50 rounded-md"
        >
          <div>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="w-4 h-4"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
              stroke-width="2"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M3 4a1 1 0 011-1h16a1 1 0 011 1v2.586a1 1 0 01-.293.707l-6.414 6.414a1 1 0 00-.293.707V17l-4 4v-6.586a1 1 0 00-.293-.707L3.293 7.293A1 1 0 013 6.586V4z"
              />
            </svg>
          </div>
          <div class="hidden sm:block">
            {{ isActive ? `Advanced Search` : `Simple search` }}
          </div>
        </span>
      </button>
    </div>
  </div>
</template>
