<script>
import SearchIcon from '../assests/search-icon.vue'
import SearchFilter from './TheFilter.vue'
import ThePagination from './ThePagination.vue'
import Modal from './email-modal.vue'

export default {
  components: { Modal, SearchFilter, ThePagination, SearchIcon },

  props: {
    tableData: {
      required: true,
      default: []
    }
  }
}
</script>

<template>
  <div class="flex flex-col">
    <div class="overflow-x-auto">
      <div class="p-1.5 w-full inline-block align-middle">
        <div class="overflow-auto border rounded-lg">
          <table class="min-w-full divide-y divide-gray-200">
            <thead class="bg-gray-100">
              <tr>
                <th class="table-header">Subject</th>
                <th class="table-header">From</th>
                <th class="table-header">To</th>
                <th class="table-header">Date</th>
                <th></th>
              </tr>
            </thead>
            <tbody v-if="this.tableData.length !== 0" class="divide-y divide-gray-200">
              <tr v-for="email in this.tableData" :key="email._id">
                <td class="table-item">
                  {{ email._source.subject }}
                </td>
                <td class="table-item">
                  {{ email._source.from }}
                </td>
                <td class="table-item">
                  {{ email._source.to.join(', ') }}
                </td>
                <td class="table-item">
                  {{ email._source.date }}
                </td>
                <td class="table-item">
                  <Modal :email="email._source"></Modal>
                </td>
              </tr>
            </tbody>
            <tbody v-else class="justify-center">
              <tr>
                <td colspan="5" class="table-cell text-gray-400 text-center text-2xl">
                  <div class="flex items-center justify-center my-10">
                    <span>Data not found</span>
                  </div>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>
