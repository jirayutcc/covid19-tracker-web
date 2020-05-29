<template>
  <v-container>
    <v-app id="app">
      <v-content>
        <v-row class="justify-center">
          <img alt="Vue logo" src="@/assets/covid19.png" />
        </v-row>
        <v-row class="justify-center">
          <h1>TRACKER WEB</h1>
        </v-row>
        <v-row class="justify-center">
          <Cards :datas="{ confirmed, recovered, deaths, lastUpdate }" />
        </v-row>
      </v-content>
    </v-app>
  </v-container>
</template>

<script>
import axios from "axios";
import Cards from "@/components/Cards";

export default {
  name: "App",
  components: {
    Cards,
  },
  data() {
    return {
      confirmed: [],
      recovered: [],
      deaths: [],
      lastUpdate: "",
    };
  },
  created() {
    axios
      .get(`https://covid19.mathdro.id/api`)
      .then((response) => {
        console.log(":= ", response.data);
        this.confirmed = response.data.confirmed;
        this.recovered = response.data.recovered;
        this.deaths = response.data.deaths;
        this.lastUpdate = response.data.lastUpdate;
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
