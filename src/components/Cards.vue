<template>
  <v-container>
    <div id="cards">
      <v-row class="justify-center">
        <v-col cols="12" md="3">
          <v-card class="text-center text-md-left">
            <v-card-subtitle class="pb-0 text-md-left">Infected</v-card-subtitle>
            <v-card-title id="title">{{ datas.confirmed.value.toLocaleString() }}</v-card-title>
            <v-card-text>
              <div>{{ new Date(datas.lastUpdate).toDateString() }}</div>
            </v-card-text>
          </v-card>
        </v-col>
        <v-col cols="12" md="3">
          <v-card class="text-center text-md-left" >
            <v-card-subtitle class="pb-0 text-md-left">Recovered</v-card-subtitle>
            <v-card-title id="title">{{ datas.recovered.value.toLocaleString() }}</v-card-title>
            <v-card-text>
              <div>{{ new Date(datas.lastUpdate).toDateString() }}</div>
            </v-card-text>
          </v-card>
        </v-col>
        <v-col cols="12" md="3">
           <v-card class="text-center text-md-left">
            <v-card-subtitle class="pb-0 text-md-left">Deaths</v-card-subtitle>
            <v-card-title id="title" class="text-center">{{ datas.deaths.value.toLocaleString() }}</v-card-title>
            <v-card-text>
              <div>{{ new Date(datas.lastUpdate).toDateString() }}</div>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </div>
  </v-container>
</template>

<script>
export default {
  name: "Cards",
  props: ["datas"],
};
</script>

<style scoped>
* {
  font-size: 18px;
}

#title {
  display: inline-flex;
  font-size: 43px;
}
</style>
