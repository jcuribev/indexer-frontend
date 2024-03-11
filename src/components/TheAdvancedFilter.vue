<script>
import searchIcon from '../assests/search-icon.vue'

export default {
  components: { searchIcon },

  name: 'AdvancedFilter',
  emits: ['formData'],

  data() {
    return {
      formData: {
        subject: '',
        body: '',
        from: '',
        to: '',
        date: '',
        messageId: ''
      },
      error: null
    }
  },
  methods: {
    submitForm() {
      if (Object.values(this.formData).some((value) => value.trim() !== '')) {
        this.$emit('form-data', this.formData)
        this.error = null
      } else {
        alert('You must fill out at least one field')
      }
    }
  }
}
</script>

<template>
  <div class="w-full py-3 pl-2">
    <form
      @submit.prevent="submitForm"
      class="flex flex-row flex-wrap justify-center gap-6 bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4"
    >
      <div class="mb-2 basis-1/3 md:grow">
        <label for="from" class="block text-gray-700 text-sm font-bold mb-2"> Subject </label>
        <input
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          type="text"
          id="name"
          v-model="formData.subject"
        />
      </div>
      <div class="mb-2 basis-1/3 md:grow">
        <label for="from" class="block text-gray-700 text-sm font-bold mb-2"> Body </label>
        <input
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          type="text"
          id="name"
          v-model="formData.body"
        />
      </div>
      <div class="mb-2 basis-1/3 md:grow">
        <label for="from" class="block text-gray-700 text-sm font-bold mb-2"> From </label>
        <input
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          type="text"
          id="name"
          v-model="formData.from"
        />
      </div>
      <div class="mb-2 basis-1/3 md:grow">
        <label for="from" class="block text-gray-700 text-sm font-bold mb-2"> To </label>
        <input
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          type="text"
          id="name"
          v-model="formData.to"
        />
      </div>
      <div class="mb-2 basis-1/3 md:grow">
        <label for="from" class="block text-gray-700 text-sm font-bold mb-2"> Date </label>
        <input
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          type="text"
          id="name"
          v-model="formData.date"
        />
      </div>
      <div class="mb-2 basis-1/3 md:grow">
        <label for="from" class="block text-gray-700 text-sm font-bold mb-2"> MessageID </label>
        <input
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          type="text"
          id="name"
          v-model="formData.messageId"
        />
      </div>
      <div class="w-full flex flex-row justify-end">
        <button
          type="submit"
          class="max-w-xs max-h-10 p-3 border rounded-md text-white dark:text-gray-800 flex items-center justify-center bg-sky-500 hover:bg-opacity-75"
        >
          <span class="mr-2 text-white">SEARCH</span>
          <searchIcon class="w-6 h-6" />
        </button>
      </div>
    </form>
  </div>
</template>
