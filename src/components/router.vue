<template>
  <div>
    <button class="btn btn-light" @click="$parent.toggleChart"  :disabled="!showReports">
      <img src="@/icons/product.png" class="icon-img"  />
      Show search products
    </button>
    <button class="btn btn-light ml-1" @click="$parent.toggleChart" :disabled="showReports">
      <img
        src="@/icons/analytics-outline.svg"
        class="icon-img"
      />
      Show search analyses
    </button>
  </div>
</template>
<style scoped>
.ml-1 {
  margin-left: 1em;
}
</style>
<script>

export default {
    props: ["showReports"]
}
</script>
