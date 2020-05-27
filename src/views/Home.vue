<template>
  <v-container>
    <div id="home">
      <img alt="Vue logo" src="../assets/covid19.png" />
      <h1>COVID19 TRACKER WEB</h1>
    </div>
  </v-container>
</template>

<script>
import axios from 'axios';

export default {
  name: "Home",
  data() {
    return {
      data: [],
      errors: []
    }
  },
  created() {
    axios.get(`https://covid19.mathdro.id/api`)
    .then(response => {
      this.data = response.data
      //console.log(":= ", this.data)
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
};
</script>
