<template>
  <div class="container">
    <h2>Visualization</h2>
    <div class="center">
      <Chart v-bind:chartData="chartData" v-bind:options="options" />
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
      layout: {
        padding: {
          //   left: 50,
          //   right: 50
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
  /* height: 50%; */
}
.center {
  margin: auto;
  max-width: 50%;
  max-height: 50%;
  min-height: 50%;
}
</style>