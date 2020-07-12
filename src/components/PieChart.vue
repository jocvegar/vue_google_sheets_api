<script>
import { Pie } from 'vue-chartjs'

export default {
    extends: Pie,
    props: {
        chartdata_pie_data_healed: {
            type: Array,
            default: null
        },
        chartdata_pie_data_deceased: {
            type: Array,
            default: null
        },
        chartdata_pie_data_better: {
            type: Array,
            default: null
        }
    },
    data() {
        return {
            chartdata: {
                labels: [
					'curados',
					'fallecidos',
					'infectados',
                ],
                datasets: [
                    {
                        backgroundColor: [
                            '#42b883',
                            '#42b840',
                            '#aab883',
                        ],
                        data: [
                            this.chartdata_pie_data_healed[0],
                            this.chartdata_pie_data_deceased[0],
                            this.chartdata_pie_data_better[0],
                        ],
                    },
                ],
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                legend: {
                    position: 'top'
                },
				title: {
					display: true,
                    text: 
                        `Total Casos: ${
                            this.chartdata_pie_data_healed[0] + 
                            this.chartdata_pie_data_deceased[0] +
                            this.chartdata_pie_data_better[0] }`
                },
                animation: {
                    animateScale: true
                }
			}
        }
    },
    mounted() {
        this.renderChart(this.chartdata, this.options)
    }
}
</script>
