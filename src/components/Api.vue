<template>
    <div id="container">
        <section v-if="errored">
            <p>No lo pude load! Try again later</p>
        </section>
        <section v-else>
            <div v-if="loading">Loading...</div>
            <div v-else>
                <div class="chart-container">
                    <line-chart  
                        :chartdata_labels="chartdata_labels"
                        :chartdata_data="chartdata_data" />
                    <br>
                    <br>
                    <pie-chart 
                        :chartdata_pie_data_healed="chartdata_pie_data_healed"
                        :chartdata_pie_data_deceased="chartdata_pie_data_deceased"
                        :chartdata_pie_data_better="chartdata_pie_data_better" />    
                    <br>
                    <br> 
                    <a class="bmc-button" target="_blank" href="https://www.buymeacoffee.com/uqlpfWJ">
                        <img src="https://cdn.buymeacoffee.com/buttons/bmc-new-btn-logo.svg" alt="Buy me a coffee">
                    </a>
                </div>
            </div>
        </section>
    </div>
</template>

<script>
import axios from 'axios';
import LineChart from './LineChart.vue'
import PieChart from './PieChart.vue'
import moment from 'moment'
moment.locale('es');

export default {
    components: { LineChart, PieChart },
    data() {
        return {
            chartdata_labels: null,
            chartdata_data: null,
            chartdata_pie_data_healed: null,
            chartdata_pie_data_deceased: null,
            chartdata_pie_data_better: null,
            loading: true,
            errored: false,
        }
    },
    async mounted() {
        axios
            .get(process.env.VUE_APP_API_LINK)
            .then(response => {
              this.chartdata_labels = response.data.cases.map(x => moment(x.date).format('DD [de] MMM'))     
              this.chartdata_data = response.data.cases.map(x => x.cases)     
              this.chartdata_pie_data_healed = response.data.cases.map(x => x.healed).filter(function(e){return e})
              this.chartdata_pie_data_deceased = response.data.cases.map(x => x.deceased).filter(function(e){return e})
              this.chartdata_pie_data_better = response.data.cases.map(x => x.better).filter(function(e){return e})
            })
            .catch(error => {
                console.log(error)
                this.errored = true
            })
            .finally(() => this.loading = false)
    },
}
</script>

<style>
.chart-container {
    margin: auto;
    height: 50vh;
    width: 90vw;
}
</style>
