<template>
  <v-container>
    <v-app id="app">
      <v-content>
        <img alt="Vue logo" src="@/assets/covid19.png" />
        <h1>COVID19 TRACKER WEB</h1>
      </v-content>
    </v-app>
  </v-container>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      data: [],
      errors: [],
    };
  },
  created() {
    axios
      .get(`https://covid19.mathdro.id/api`)
      .then((response) => {
        this.data = response.data;
        //console.log(":= ", this.data)
      })
      .catch((e) => {
        this.errors.push(e);
      });
  },
};
</script>

<style scoped>
* {
  font-family: "Jua", sans-serif;
}
</style>
