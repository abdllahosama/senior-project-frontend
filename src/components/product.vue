<template>
  <div class="col-md-6 mt-2 mb-2">
      <ul class="list-group">
        <li class="list-group-item">
          {{ product.product }}
        </li>
        <li class="list-group-item">
          {{ product.category }}
        </li>
        <li class="list-group-item">
          {{ product.brand }}
        </li>
      </ul>
  </div>
</template>
<script>
export default {
  props: ["product"],
};
</script>
