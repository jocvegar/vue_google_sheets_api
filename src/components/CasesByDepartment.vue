<template>
    <div class="horizontal-chart" ref="bydepartmentdiv"></div>
</template>

<script>
import * as am4core from "@amcharts/amcharts4/core";
import * as am4charts from "@amcharts/amcharts4/charts";
import am4themes_spiritedaway from "@amcharts/amcharts4/themes/spiritedaway";
import am4themes_animated from "@amcharts/amcharts4/themes/animated";

export default {
    name: 'CasesByDepartment',
    props: {
        by_department: {
            type: Object,
            default: null
        },
    },
    mounted() {
        am4core.useTheme(am4themes_spiritedaway);
        am4core.useTheme(am4themes_animated);

        let chart = am4core.create(this.$refs.bydepartmentdiv, am4charts.XYChart);
        chart.hiddenState.properties.opacity = 0; // this creates initial fade-in

        let title = chart.titles.create();
        title.text = "Casos por Departamento";
        title.marginBottom = "10";

        let categoryAxis = chart.xAxes.push(new am4charts.CategoryAxis());
        categoryAxis.renderer.grid.template.location = 0;
        categoryAxis.dataFields.category = "departamento";
        categoryAxis.renderer.labels.template.horizontalCenter = "right";
        categoryAxis.renderer.labels.template.verticalCenter = "middle";
        categoryAxis.renderer.labels.template.rotation = 270;
        categoryAxis.renderer.minGridDistance = 5;
        categoryAxis.fontSize = 12;

        let valueAxis = chart.yAxes.push(new am4charts.ValueAxis());
        valueAxis.min = 0;
        valueAxis.max = 10000;
        valueAxis.strictMinMax = true;
        valueAxis.renderer.minGridDistance = 20;
        valueAxis.renderer.labels.template.fontSize = 12;

        let axisBreak = valueAxis.axisBreaks.create();
        axisBreak.startValue = 700;
        axisBreak.endValue = 9000;

        // fixed axis break
        let d = (axisBreak.endValue - axisBreak.startValue) / (valueAxis.max - valueAxis.min);
        axisBreak.breakSize = 0.05 * (1 - d) / d; // 0.05 means that the break will take 5% of the total value axis height

        // make break expand on hover
        let hoverState = axisBreak.states.create("hover");
        hoverState.properties.breakSize = 1;
        hoverState.properties.opacity = 0.1;
        hoverState.transitionDuration = 1500;

        axisBreak.defaultState.transitionDuration = 1000;

        let series = chart.series.push(new am4charts.ColumnSeries());
        series.dataFields.categoryX = "departamento";
        series.dataFields.valueY = "casos";
        series.columns.template.tooltipText = "{categoryX}: {valueY}";
        series.columns.template.tooltipY = 0;
        series.columns.template.strokeOpacity = 0;

        series.columns.template.adapter.add("fill", function(fill, target) {
            return chart.colors.getIndex(target.dataItem.index);
        });

        categoryAxis.sortBySeries = series;

        chart.data = [
            {
                "departamento": "Atlantida",
                "casos": this.by_department["atlantida"]
            },
            {
                "departamento": "Choluteca",
                "casos": this.by_department["choluteca"]
            },
            {
                "departamento": "Colón",
                "casos": this.by_department["colon"]
            },
            {
                "departamento": "Comayagua",
                "casos": this.by_department["comayagua"]
            },
            {
                "departamento": "Copán",
                "casos": this.by_department["copan"]
            },
            {
                "departamento": "Cortés",
                "casos": this.by_department["cortes"]
            },
            {
                "departamento": "El Paraíso",
                "casos": this.by_department["el_paraiso"]
            },
            {
                "departamento": "Franciso Morazán",
                "casos": this.by_department["fm"]
            },
            {
                "departamento": "Gracias a Dios",
                "casos": this.by_department["gracias_a_dios"]
            },
            {
                "departamento": "Intibuca",
                "casos": this.by_department["intibuca"]
            },
            {
                "departamento": "Islas de la Bahía",
                "casos": this.by_department["islas"]
            },
            {
                "departamento": "La Paz",
                "casos": this.by_department["la_paz"]
            },
            {
                "departamento": "Lempira",
                "casos": this.by_department["lempira"]
            },
            {
                "departamento": "Ocotepeque",
                "casos": this.by_department["ocotepeque"]
            },
            {
                "departamento": "Olancho",
                "casos": this.by_department["olancho"]
            },
            {
                "departamento": "Santa Barbara",
                "casos": this.by_department["santa_barbara"]
            },
            {
                "departamento": "Valle",
                "casos": this.by_department["valle"]
            },
            {
                "departamento": "Yoro",
                "casos": this.by_department["yoro"]
            },
        ]
    },
    beforeDestroy() {
        if (this.chart) {
            this.chart.dispose();
        }
    }    
}
</script>

<style>
.horizontal-chart {
    height: 90vh;
}
</style>

