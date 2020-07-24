<template>
  <v-container>
    <v-app id="app">
      <v-content>
        <br />
        <v-row class="justify-center">
          <v-lazy min-height="100" transition="scale-transition">
            <img src="@/assets/covid19.png" />
          </v-lazy>
        </v-row>
        <v-row class="justify-center">
          <Cards :cardsData="{ confirmed, recovered, deaths, lastUpdate }" />
        </v-row>
        <br>
        <v-row class="justify-center">
          <Chart :chartData="{ confirmed, recovered, deaths }"/>
        </v-row>
      </v-content>
    </v-app>
  </v-container>
</template>

<script>
import axios from "axios";
import Cards from "@/components/Cards";
import Chart from "@/components/Chart";

export default {
  name: "App",
  components: {
    Cards,
    Chart
  },
  data() {
    return {
      confirmed: [],
      recovered: [],
      deaths: [],
      lastUpdate: ""
    };
  },
  created() {
    axios
      .get(`https://covid19.mathdro.id/api`)
      .then(({ data }) => {
        this.confirmed = data.confirmed;
        this.recovered = data.recovered;
        this.deaths = data.deaths;
        this.lastUpdate = data.lastUpdate;
      })
      .catch((e) => {
        console.error("error : ", e);
      });
  },
};
</script>

<style scoped>
* {
  font-family: "Bebas Neue", cursive;
}
</style>
