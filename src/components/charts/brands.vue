<template>
  <div>
    <div class="card">
      <div class="card-header">Products per brand</div>
      <div class="card-body">
        <canvas id="brandsCahrt"></canvas>
      </div>
    </div>
  </div>
</template>
<script>
import Chart from "chart.js/auto";

export default {
  props: ["data"],
  mounted() {
    new Chart(document.getElementById("brandsCahrt"), {
      type: "line",
      options: {
        responsive: true,
        plugins: {},
      },
      data: {
        labels: ["brand-1", "brand-2", "brand-3"],
        datasets: [
          {
            label: "product",
            data: this.data,
            borderColor: "#ff6384",
            backgroundColor: "#ff638499",
            pointStyle: "circle",
            pointRadius: 10,
            pointHoverRadius: 15,
          },
        ],
      },
    });
  },
};
</script>
