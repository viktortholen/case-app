<script>
import { Bubble } from "vue-chartjs";
import { scaleLinear } from "d3";
//TODO: Color code indexChange (blue -> red scale)

export default {
  extends: Bubble,
  name: "bubble-chart",
  props: ["chartData", "options"],
  mounted() {
    let radiusScale = scaleLinear().domain([0, 30]).range([5, 40]);
    let parsedData = this.chartData.map((d) => ({
      x: d.index,
      y: d.responseRate,
      r: radiusScale(d.employees),
      name: d.name,
      change: d.indexChange
    }));
    delete parsedData[0];
    this.renderChart(
      {
        datasets: [
          {
            label: "Data",
            data: parsedData,
            backgroundColor: "rgba(20, 60, 100, 0.7)",
          },
        ],
      },
      this.options
    );
  },
};
</script>

<style scoped>
</style>