<template>
  <div>
    <noResult v-if=" products.length == 0"/>
    <template  v-if=" products.length > 0">
      <h3 class="text-center mt-3" id="productsCount">{{totalItems}}  Result founded</h3>
      <div class="row mt-3" id="itemsTarget">
          <product v-for="(product, index) in products" :key="index" :product="product" />
      </div>
      <div class=" text-center">
          <button class="btn btn-primary p-2 m-3 w-50" id="loadMore" @click="$parent.getItems()" :disabled="loading" v-if="totalPages > currentPage">
            <div class="spinner-border" role="status" v-if="loading">
              <span class="sr-only"></span>
            </div>
            {{loading ? '' : 'load more'}}
          </button>
      </div>
    </template>
  </div>
</template>

<script>
import product from '@/components/product.vue'
import noResult from '@/components/noResult.vue'
export default {
  name: 'HelloWorld',
  props: ["products", "totalPages", "currentPage", "totalItems", "loading"],
  components: {
    product,
    noResult
  }
}
</script>