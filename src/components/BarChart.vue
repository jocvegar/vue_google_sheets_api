<script>
import { Bar } from 'vue-chartjs'

export default {
    extends: Bar,
    props: {
        chartdata_labels: {
            type: Array,
            default: null
        },
        chartdata_bar_data_by_day: {
            type: Array,
            default: null
        }
    },
    data() {
        return {
            chartdata: {
                labels: this.chartdata_labels,
                datasets: [
                    {   
                        label: "Casos Por Evento",
                        backgroundColor: 'rgba(255, 145, 113, 0.2)',
                        borderColor: 'rgb(255, 145, 113)',
                        data: this.chartdata_bar_data_by_day,
                        borderWidth: 1,
                    },
                ],
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
				tooltips: {
					mode: 'index',
					intersect: false,
                },
			}
        }
    },
    mounted() {
        this.renderChart(this.chartdata, this.options)
    }
}
</script>
