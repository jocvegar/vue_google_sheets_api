<template>
    <div id="container">
        <section v-if="errored">
            <p>No lo pude load! Try again later</p>
        </section>
        <section v-else>
            <div v-if="loading" class="loading-container">Conectándome a la base de batos...</div>
            <div v-else>
                <div class="chart-container">
                     <department-map 
                        :by_department="by_department" />
                    <br>
                    <br>
                    <cases-by-department
                        :by_department="by_department" />
                    <br>
                    <br>
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
                     <bar-chart  
                        :chartdata_labels="chartdata_labels"
                        :chartdata_bar_data_by_day="chartdata_bar_data_by_day" />
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
import BarChart from './BarChart.vue'
import DepartmentMap from './DepartmentMap.vue'
import CasesByDepartment from './CasesByDepartment.vue'
import moment from 'moment'
moment.locale('es');

export default {
    components: { LineChart, PieChart, BarChart, DepartmentMap, CasesByDepartment },
    data() {
        return {
            chartdata_labels: null,
            chartdata_data: null,
            chartdata_pie_data_healed: null,
            chartdata_pie_data_deceased: null,
            chartdata_pie_data_better: null,
            chartdata_bar_data_by_day: null,
            loading: true,
            errored: false,
            by_department: null,
        }
    },
    async mounted() {
        axios
            .get(process.env.VUE_APP_API_LINK)
            .then(response => {
                this.response = response
                this.chartdata_labels = response.data.cases.map(x => moment(x.date).format('DD [de] MMM'))     
                this.chartdata_data = response.data.cases.map(x => x.cases)     
                this.chartdata_pie_data_healed = response.data.cases.map(x => x.healed).filter(function(e){return e})
                this.chartdata_pie_data_deceased = response.data.cases.map(x => x.deceased).filter(function(e){return e})
                this.chartdata_pie_data_better = response.data.cases.map(x => x.better).filter(function(e){return e})
                this.chartdata_bar_data_by_day = response.data.cases.map(x => x.cases_by_day)
                this.by_department = response.data.cases[0]
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
    height: 60vh;
    width: 90vw;
}
.loading-container {
    padding:2rem 0;
}
</style>
