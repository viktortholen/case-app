<script>
import { Bubble } from "vue-chartjs";

export default {
  extends: Bubble,
  name: "bubble-chart",
  props: ["chartData", "options"],
  mounted() {
    this.renderChart(
      {
        datasets: [
          {
            data: this.chartData,
            backgroundColor: (d) => {
              return d.dataset.data[d.dataIndex] ? d.dataset.data[d.dataIndex].color : "";
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