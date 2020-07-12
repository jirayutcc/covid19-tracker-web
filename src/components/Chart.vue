<template>
  <div id="chart">
    <canvas id="graph" width="400" height="400"></canvas>
  </div>
</template>

<script>
import axios from "axios";
import Chart from "chart.js";

export default {
  name: "Chart",
  props: ["chartData"],
  mounted: function() {
    axios
      .get(`https://covid19.mathdro.id/api`)
      .then(({ data }) => {
        var ctx = document.getElementById("graph").getContext("2d");
        var bar = new Chart(ctx, {
          type: "pie",
          data: {
            labels: ["confirmed", "recovered", "deaths"],
            datasets: [
              {
                label: "#",
                data: [
                  data.confirmed.value,
                  data.recovered.value,
                  data.deaths.value,
                ],
                backgroundColor: ["#3498DB", "#1ABC9C", "#E74C3C"],
              },
            ],
          },
        });
        console.log(bar);
      })
      .catch((e) => {
        console.error("error : ", e);
      });
  },
};
</script>

<style scoped></style>
