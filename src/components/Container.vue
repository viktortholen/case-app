<template>
  <div class="container">
    <h2>Visualization</h2>
    <div class="center">
      <Chart
        :chartData="chartData"
        :options="options"
        :height="500"
      />
    </div>
  </div>
</template>

<script>
import Chart from "./Chart.vue";
import employee_data from "../data/data.json";

export default {
  name: "Container",
  data: () => ({
    chartData: employee_data,
    options: {
      responsive: true,
      maintainAspectRatio: false,
      title: "Visualization of Company Management",
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
              labelString: "Response Rate",
            },
            ticks: {
              suggestedMin: 0,
            },
          },
        ],
        xAxes: [
          {
            scaleLabel: {
              display: true,
              labelString: "Index",
            },
            // ticks: {
            //   suggestedMin: 0,
            // },
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
            return "Index: " + item.x + " ( " + change + " )";
          },
          afterLabel: function (tooltipItem, data) {
            let item =
              data.datasets[tooltipItem.datasetIndex].data[tooltipItem.index];
            return ["ResponseRate: " + item.y, "Employees: " + item.employees];
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
.center {
  margin: auto;
  max-width: 60%;
}
</style>