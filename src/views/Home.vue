<script>
import axios from 'axios'
import TheFilter from '../components/TheFilter.vue'
import ThePagination from '../components/ThePagination.vue'
import TheTable from '../components/TheTable.vue'
export default {
  components: { TheFilter, TheTable, ThePagination },

  data: () => {
    return {
      tableData: [],
      url: 'http://localhost:3000/api',
      listEndpoint: '/list',
      searchEndpoint: '/search',
      advancedSearchEndpoint: '/advancedSearch',
      elementsPerPage: 10,
      data: null,
      currentFilters: {
        subject: '',
        body: '',
        from: '',
        to: '',
        date: '',
        messageId: ''
      },
      totalResults: 0
    }
  },

  mounted() {
    this.getInitialData()
  },

  methods: {
    setTableData(data) {
      this.tableData = data
    },

    onChangePage(page) {
      this.handleSearchRouting(this.currentFilters, page)
    },

    handleSearchRouting(searchData, page = 0) {
      if (searchData === '') this.getInitialData(page)
      else if (typeof searchData === 'string') this.makeSimpleSearch(searchData, page)
      else if (typeof searchData === 'object') this.makeAdvancedSearch(searchData, page)
    },

    getInitialData(page = 0) {
      this.makeAndHandleRequest('', page, this.url + this.listEndpoint)
    },

    makeSimpleSearch(searchData, page) {
      this.makeAndHandleRequest(searchData, page, this.url + this.searchEndpoint)
    },

    makeAdvancedSearch(searchData, page) {
      this.makeAndHandleRequest(searchData, page, this.url + this.advancedSearchEndpoint)
    },

    async makeAndHandleRequest(searchData, page, url) {
      const requestBody = this.createRequest(searchData, page)
      const response = await this.fetchData(requestBody, url)
      const responseResult = this.handleResponse(response)

      if (responseResult[0]) this.onSuccessfulQuery(response, searchData)
      else this.onErrorQuery(responseResult[1])
    },

    createRequest(searchData = this.currentFilters, page, targetEndpoint) {
      let requestBody = {
        searchData: searchData,
        page: page,
        elementsPerPage: this.elementsPerPage
      }

      try {
        requestBody = JSON.stringify(requestBody)
      } catch (error) {
        alert('An error has ocurred', error)
        return null
      }

      return requestBody
    },

    async fetchData(requestBody, url) {
      console.log(requestBody)
      console.log(url)
      const response = await axios.post(url, requestBody, {
        headers: {
          Accept: 'application/json',
          'Content-Type': 'application/json;charset=UTF-8'
        }
      })

      return response
    },

    handleResponse(response) {
      console.log(response)
      if (response.status === 200) {
        return [true, '']
      } else if (response.status) {
        return [false, `Data couldn't be fetched`]
      } else {
        return [false, response]
      }
    },

    onSuccessfulQuery(response, searchData) {
      this.currentFilters = searchData
      this.totalResults = response.data.hits.total.value
      this.setTableData(response.data.hits.hits)
    },

    onErrorQuery(error) {
      alert(error)
    }
  }
}
</script>

<template>
  <div class="flex flex-col">
    <TheFilter @search-input="this.handleSearchRouting" />
    <TheTable :tableData="this.tableData" />
    <div class="self-center">
      <ThePagination
        @change-page="onChangePage"
        :total="this.totalResults"
        :perPage="this.elementsPerPage"
      ></ThePagination>
    </div>
  </div>
</template>
