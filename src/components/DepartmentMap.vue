<template>
  <div class="map" ref="chartdiv">
  </div>
</template>

<script>
import * as am4core from "@amcharts/amcharts4/core";
import * as am4maps from "@amcharts/amcharts4/maps";
import am4geodata_hondurasLow from "@amcharts/amcharts4-geodata/hondurasLow";

export default {
    name: 'DepartmentMap',
     props: {
        by_department: {
            type: Object,
            default: null
        },
    },
    mounted() {
        let map = am4core.create(this.$refs.chartdiv, am4maps.MapChart);
        map.geodata = am4geodata_hondurasLow;
        map.projection = new am4maps.projections.Miller();

        let polygonSeries = new am4maps.MapPolygonSeries();
        polygonSeries.useGeodata = true;
        map.series.push(polygonSeries);

        polygonSeries.data = 
        [ 
            {
                "id": "HN-AT",
                "value": this.by_department["atlantida"]
            },
            {
                "id": "HN-CH",
                "value": this.by_department["choluteca"]
            },
            {
                "id": "HN-CL",
                "value": this.by_department["colon"]
            },
            {
                "id": "HN-CM",
                "value": this.by_department["comayagua"]
            },
            {
                "id": "HN-CP",
                "value": this.by_department["copan"]
            },
            {
                "id": "HN-CR",
                "value": this.by_department["cortes"]
            },
            {
                "id": "HN-EP",
                "value": this.by_department["el_paraiso"]
            },
            {
                "id": "HN-FM",
                "value": this.by_department["fm"]
            },
            {
                "id": "HN-GD",
                "value": this.by_department["gracias_a_dios"]
            },
            {
                "id": "HN-IN",
                "value": this.by_department["intibuca"]
            },
            {
                "id": "HN-IB",
                "value": this.by_department["islas"]
            },
            {
                "id": "HN-LP",
                "value": this.by_department["la_paz"]
            },
            {
                "id": "HN-LM",
                "value": this.by_department["lempira"]
            },
            {
                "id": "HN-OC",
                "value": this.by_department["ocotepeque"]
            },
            {
                "id": "HN-OL",
                "value": this.by_department["olancho"]
            },
            {
                "id": "HN-SB",
                "value": this.by_department["santa_barbara"]
            },
            {
                "id": "HN-VA",
                "value": this.by_department["valle"]
            },
            {
                "id": "HN-YO",
                "value": this.by_department["yoro"]
            },
        ];

        let polygonTemplate = polygonSeries.mapPolygons.template;
        polygonTemplate.tooltipText = "{name}: {value}";
        polygonTemplate.fill = am4core.color("#74B266");

        let hs = polygonTemplate.states.create("hover");
        hs.properties.fill = am4core.color("#367B25");
    },
    beforeDestroy() {
        if (this.map) {
            this.map.dispose();
        }
    }
}
</script>

<style scoped>
.map {
    width: 100%;
    height: 300px;
}
</style>
