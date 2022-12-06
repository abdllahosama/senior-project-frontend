<template>
  <div class="container mt-3">
    <div class="row">
      <div class="col-md-4">
        <sidebar 
          :filter="filter" 
          :brands="brands"
          :categories="categories"
          />
      </div>
      <div class="col-md-8">
        <router :showReports="showReports" />
        <maiLoading v-if="mainLoading" />
        <reportsContainer :reportData="reportData"  v-if="!mainLoading && showReports" />
        <productsContainer 
          :products="products" 
          :totalPages="totalPages" 
          :currentPage="currentPage" 
          :totalItems="totalItems" 
          :loading="loading"
          v-if="!mainLoading && !showReports"
        />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

import sidebar from '@/components/sidebar.vue'
import productsContainer from '@/components/productsContainer.vue'
import reportsContainer from '@/components/reportsContainer.vue'

import maiLoading from '@/components/maiLoading'
import router from '@/components/router.vue'

export default {
  name: 'App',
  data () {
    return {
      products: [],
      reportData: {
        categories: [],
        brands: []
      },
      totalItems: 0,
      currentPage: 0,
      totalPages: 0,
      loading: false,
      mainLoading: false,
      showReports: false,
      filter: {
        search: "",
        categories: [],
        brands: []
      },
      brands: ['brand-1', 'brand-2', 'brand-3'],
      categories: ['category-1', 'category-2', 'category-3']
    }
  },
  methods: {
    async getItems () {
      this.loading = true
      this.currentPage += 1
      await axios.get('/api/getproducts', { params: {...this.filter, page: this.currentPage}})
      .then((response) => {
        this.products.push(...response.data.items.data)
        this.totalItems = response.data.items.total
        this.totalPages = response.data.items.last_page
        this.loading = false
      })
      await axios.get('/api/getproductsanalytics', { params: this.filter})
      .then((response) => {
        this.reportData = response.data.data
      })

      this.mainLoading = false
      
    },
    changeFilter () {
      this.currentPage = 0
      this.products=[]
      this.mainLoading = true
      this.getItems()
    },
    toggleChart () {
      this.showReports = !this.showReports
    }
  },
  mounted () {
    this.mainLoading = true
    this.getItems()
  },
  watch: {
    filter: {
      deep: true,
      handler(){
        this.changeFilter()
      }
    }
  },
  components: {
    sidebar,
    productsContainer,
    reportsContainer,
    maiLoading,
    router
  }
}
</script>

<style>
body {
  background: #eee !important;
}
.icon-img {
  width:30px;
  margin-right: 4px;
}
</style>
