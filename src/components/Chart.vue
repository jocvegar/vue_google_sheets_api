<script>
import { Line } from 'vue-chartjs'

export default {
    extends: Line,
    data() {
        return {
            info: null,
            loading: true,
            errored: false,
            chartdata: {
                labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July'],
                datasets: [{
					label: 'My First dataset',
					data: [
						3,
						10,
						15,
						30,
						90,
						110,
						249
					],
					fill: false,
				}]
            },
            options: {
				responsive: true,
				title: {
					display: true,
					text: 'Chart.js Line Chart'
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
							labelString: 'Month'
						}
					}],
					yAxes: [{
						display: true,
						scaleLabel: {
							display: true,
							labelString: 'Hola'
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

<style>

</style>
