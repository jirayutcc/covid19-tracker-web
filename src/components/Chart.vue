<template>
  <div id="chart">
    <canvas id="graph" width="400" height="400"></canvas>
  </div>
</template>

<script>
import Chart from "chart.js";

export default {
  name: "Chart",
  props: ["chartData"],
  data() {
    return {
      chart: null,
    };
  },
  mounted() {
    this.renderChart();
  },
  watch: {
    chartData() {
      this.renderChart();
    },
  },
  beforeDestroy() {
    if (this.chart) {
      this.chart.destroy();
    }
  },
  methods: {
    renderChart() {
      if (!this.chartData) {
        return;
      }

      var ctx = document.getElementById("graph").getContext("2d");

      if (this.chart) {
        this.chart.destroy();
      }

      this.chart = new Chart(ctx, {
        type: "pie",
        data: {
          labels: ["confirmed", "recovered", "deaths"],
          datasets: [
            {
              label: "#",
              data: [
                this.chartData.cases || 0,
                this.chartData.recovered || 0,
                this.chartData.deaths || 0,
              ],
              backgroundColor: ["#3498DB", "#1ABC9C", "#E74C3C"],
            },
          ],
        },
        options: {
          responsive: true,
          maintainAspectRatio: false,
        },
      });
    },
  },
};
</script>

<style scoped>
#chart {
  height: 360px;
}
</style>
