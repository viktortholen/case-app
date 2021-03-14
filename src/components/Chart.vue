<script>
import { Bubble } from "vue-chartjs";
import * as d3 from "d3";

export default {
  extends: Bubble,
  name: "bubble-chart",
  props: ["chartData", "options"],
  mounted() {
    let radiusScale = d3.scaleLinear().domain([0, 30]).range([5, 40]);
    var colorScale = d3
      .scaleLinear()
      .domain([-100, -10, -5, -1, 0, 1, 5, 10, 100])
      .range([
        "rgba(255, 0,   0,   0.8)",
        "rgba(252, 74,  38,  0.8)",
        "rgba(255, 155, 112, 0.8)",
        "rgba(255, 196, 171, 0.8)",
        "rgba(190, 190, 190, 0.8)",
        "rgba(186, 255, 186, 0.8)",
        "rgba(138, 255, 138, 0.8)",
        "rgba(84,  255, 84,  0.8)",
        "rgba(17,  255, 0,   0.8)",
      ]);

    let parsedData = this.chartData.map((d) => ({
      x: d.index ? d.index : null, // change if we want to display missing values as 0
      y: d.responseRate,
      r: radiusScale(d.employees),
      name: d.name,
      change: d.indexChange ? d.indexChange : "-",
      employees: d.employees,
      color: d.indexChange ? colorScale(d.indexChange) : "rgba(0,0,0,0.8)",
    }));
    //First element is the whole company
    delete parsedData[0];

    this.renderChart(
      {
        datasets: [
          {
            label: "Data",
            data: parsedData,
            backgroundColor: (d) => {
              if (!d.dataset.data[d.dataIndex]) {
                return;
              }
              return d.dataset.data[d.dataIndex].color;

            },
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