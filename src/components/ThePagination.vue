<script>
export default {
  props: {
    total: {
      type: Number,
      required: true
    },

    perPage: {
      type: Number,
      required: true
    }
  },

  data: () => {
    return {
      currentPage: 0
    }
  },

  computed: {
    pages() {
      if (this.perPage === 0) return 0

      return this.total / (this.perPage + 1)
    },
    isInFirstPage() {
      return this.currentPage === 0
    },
    isInLastPage() {
      return this.currentPage === this.pages
    }
  },

  methods: {
    changeToFirstPage() {
      this.currentPage = 0
      this.$emit('change-page', this.currentPage)
    },
    changeToPreviousPage() {
      this.currentPage -= 1
      this.$emit('change-page', this.currentPage * this.perPage)
    },
    changeToNextPage() {
      this.currentPage += 1
      this.$emit('change-page', this.currentPage * this.perPage)
    },
    changeToLastPage() {
      this.currentPage = this.totalPages
      this.$emit('change-page', this.currentPage)
    }
  }
}
</script>

<template>
  <div class="flex">
    <button
      @click="changeToFirstPage"
      :disabled="isInFirstPage"
      class="pagination-button flex"
      :class="{ 'cursor-not-allowed': isInFirstPage }"
    >
      &lt;&lt;
    </button>

    <button
      @click="changeToPreviousPage"
      :disabled="isInFirstPage"
      class="pagination-button flex"
      :class="{ 'cursor-not-allowed': isInFirstPage }"
    >
      &lt;-
    </button>

    <span class="mx-2 rounded-md border-2 px-3 py-2 text-base">{{ currentPage + 1 }}</span>

    <button
      @click="changeToNextPage"
      :disabled="isInLastPage"
      class="pagination-button flex"
      :class="{ 'cursor-not-allowed': isInLastPage }"
    >
      -&gt;
    </button>

    <button
      @click="changeToLastPage"
      :disabled="isInLastPage"
      class="pagination-button flex"
      :class="{ 'cursor-not-allowed': isInLastPage }"
    >
      &gt;&gt;
    </button>
  </div>
</template>
