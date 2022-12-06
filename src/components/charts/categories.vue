<template>
    <div>
        <div class="card  mt-3 mb-3">
            <div class="card-header">
                products per category
            </div>
            <div class="card-body">
                <canvas id="categoriesCahrt"></canvas>
            </div>
        </div>
    </div>
</template>
<script>
import Chart from 'chart.js/auto'

export default {
    props: ["data"],
    mounted () {
    new Chart(
      document.getElementById('categoriesCahrt'),
            {
            type: 'line',
            options: {
                    responsive: true,
                    plugins: {
                }
            },
            data: {
                    labels: ['category-1', 'category-2', 'category-3'],
                    datasets: [
                    {
                        label: 'product',
                        data: this.data,
                        borderColor: '#ff6384',
                        backgroundColor: "#ff638499",
                        pointStyle: 'circle',
                        pointRadius: 10,
                        pointHoverRadius: 15
                    }
                    ]
                }
            }
        )
    }
}
</script>
