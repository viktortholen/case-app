<template>
  <div class="container">
    <Chart :chartData="chartData" :options="options" :height="500" />
  </div>
</template>

<script>
import Chart from "./Chart.vue";
import employee_data from "../data/data.json";
import { scaleLinear } from "d3";

//Scales
let radiusScale = scaleLinear().domain([0, 30]).range([5, 40]);
var colorScale = scaleLinear()
  .domain([-100, -10, -5, -1, 1, 5, 10, 100])
  .range([
    "rgba(255, 0,   0,   1.0)",
    "rgba(252, 100, 100, 1.0)",
    "rgba(255, 138, 138, 1.0)",
    "rgba(255, 186, 186, 1.0)",
    "rgba(186, 255, 186, 1.0)",
    "rgba(138, 255, 138, 1.0)",
    "rgba(100, 255, 100, 1.0)",
    "rgba(0,   255, 0,   1.0)",
  ]);

//handle data to fit chartJS format:
let parsedData = employee_data.map((d) => ({
  x: d.responseRate,
  y: d.index ? d.index : null, // change "null" if we want to display missing values
  r: radiusScale(d.employees),
  name: d.name,
  change: d.indexChange ? d.indexChange : "-",
  employees: d.employees,
  color: d.indexChange ? colorScale(d.indexChange) : "rgba(0,0,0,0.4)",
}));
//remove the company entity from the data
delete parsedData[0];

export default {
  name: "Container",
  data: () => ({
    chartData: parsedData,
    options: {
      responsive: true,
      maintainAspectRatio: false,
      title: {
        display: true,
        text: "Visualization of Company Management",
      },
      legend: {
        display: false,
      },
      layout: {
        padding: {
          top: 50,
        },
      },
      scales: {
        yAxes: [
          {
            scaleLabel: {
              display: true,
              labelString: "Index",
            },
            ticks: {
              suggestedMin: 0,
              suggestedMax: 100,
            },
          },
        ],
        xAxes: [
          {
            scaleLabel: {
              display: true,
              labelString: "Response Rate",
            },
          },
        ],
      },
      tooltips: {
        callbacks: {
          title: function (tooltipItem, data) {
            let item =
              data.datasets[tooltipItem[0].datasetIndex].data[
                tooltipItem[0].index
              ];
            return item.name;
          },
          label: function (tooltipItem, data) {
            let item =
              data.datasets[tooltipItem.datasetIndex].data[tooltipItem.index];
            let change = item.change > 0 ? "+" + item.change : item.change;
            return "Index: " + item.y + " ( " + change + " )";
          },
          afterLabel: function (tooltipItem, data) {
            let item =
              data.datasets[tooltipItem.datasetIndex].data[tooltipItem.index];
            return ["Response Rate: " + item.x, "Employees: " + item.employees];
          },
        },
      },
    },
  }),
  components: {
    Chart,
  },
};
</script>

<style scoped>
.container {
  margin: auto;
  max-width: 60%;
}
</style>