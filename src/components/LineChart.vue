<script>
import { Line } from 'vue-chartjs'

export default {
    extends: Line,
    props: {
        chartdata_labels: {
            type: Array,
            default: null
        },
        chartdata_data: {
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
                        label: 'Casos',
                        backgroundColor: '#42b883',
                        borderColor: '#42b883',
                        data: this.chartdata_data,
                        fill: false,
                    },
                ],
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
				title: {
					display: true,
					text: 'Honduras COVID-19'
				},
				tooltips: {
					mode: 'index',
					intersect: false,
				},
				hover: {
					mode: 'nearest',
					intersect: true
				},
				scales: {
					xAxes: [{
						display: true,
						scaleLabel: {
							display: true,
							labelString: 'Fecha'
						}
					}],
					yAxes: [{
						display: true,
						scaleLabel: {
							display: true,
							labelString: 'Cantidad'
						}
					}]
				}
			}
        }
    },
    mounted() {
        this.renderChart(this.chartdata, this.options)
    }
}
</script>
