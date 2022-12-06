<template>
  <div class="card mb-3" id="sidebar">
    <div class="card-body">
      <div class="form-group">
        <input
          type="search"
          v-model="filter.search"
          class="form-control"
          placeholder="Serarch for product"
        />
      </div>
      <div class="categories-container mt-3">
        <h4>Categories</h4>
        <div
          class="form-check"
          v-for="(category, index) in categories"
          :key="index"
        >
          <input
            :id="'category' + index"
            class="form-check-input"
            type="checkbox"
            @change="toggleCategory(category)"
          />
          <label class="form-check-label" :for="'category' + index">
            {{ category }}
          </label>
        </div>
      </div>
      <div class="brands-container mt-3">
        <h4>Brands</h4>
        <div class="form-check" v-for="(brand, index) in brands" :key="index">
          <input
            :id="'brand' + index"
            class="form-check-input"
            type="checkbox"
            @change="toggleBrand(brand)"
          />
          <label class="form-check-label" :for="'brand' + index">
            {{ brand }}
          </label>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: ["filter", "brands", "categories"],
  methods: {
    toggleBrand(brand) {
      if (this.filter.brands.includes(brand)) {
        this.filter.brands.splice(this.filter.brands.indexOf(brand), 1);
      } else {
        this.filter.brands.push(brand);
      }
    },
    toggleCategory(category) {
      if (this.filter.categories.includes(category)) {
        this.filter.categories.splice(
          this.filter.categories.indexOf(category),
          1
        );
      } else {
        this.filter.categories.push(category);
      }
    },
    resizeSidebar() {
        let sidebar = document.getElementById('sidebar')
        sidebar.style.width = (sidebar.parentElement.clientWidth - 24) + "px";
    },
  },
  mounted() {
    this.resizeSidebar()
    let main = this
    window.onresize = function() {
        main.resizeSidebar()
    };
  },
};
</script>
<style scoped>
.card {
  position: fixed;
}
@media (max-width: 768px) {
    .card {
        position: unset;
      }
}
</style>