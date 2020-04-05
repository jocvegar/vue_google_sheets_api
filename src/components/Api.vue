<template>
    <div id="app">
        <section v-if="errored">
            <p>No lo pude load! Try again later</p>
        </section>
        <section v-else>
            <div v-if="loading">Loading...</div>
            <div v-else >
                 <div class="chart-container">
                     <line-chart  
                    :chartdata_labels="chartdata_labels"
                    :chartdata_data="chartdata_data" />
                 </div>
            </div>
        </section>    
    </div>
</template>

<script>
import axios from 'axios';
import LineChart from './LineChart.vue'
import moment from 'moment'
moment.locale('es');

export default {
    components: { LineChart },
    data() {
        return {
            chartdata_labels: null,
            chartdata_data: null,
            loading: true,
            errored: false,
            height: 300,
        }
    },
    async mounted() {
        axios
            .get(process.env.VUE_APP_API_LINK)
            .then(response => {
              this.chartdata_labels = response.data.cases.map(x => moment(x.date).format('DD [de] MMM'))     
              this.chartdata_data = response.data.cases.map(x => x.cases)     
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
    position: relative;
    margin: auto;
    height: 50vh;
    width: 90vw;
}
</style>
