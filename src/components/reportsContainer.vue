<template>
  <div class="row mt-3">
    <brands class="col-12" :data="reportData.brands" v-if="refrush" />
    <categories class="col-12" :data="reportData.categories" v-if="refrush" />
  </div>
</template>
<script>
import brands from "@/components/charts/brands";
import categories from "@/components/charts/categories";
export default {
  props: ["reportData"],
  data() {
    return {
      refrush: true,
    };
  },
  components: {
    brands,
    categories,
  }
};
</script>
