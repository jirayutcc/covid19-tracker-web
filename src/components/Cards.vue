<template>
  <v-container>
    <div id="cards">
      <v-row class="justify-center">
        <v-col cols="12" md="3">
          <v-lazy min-height="100" transition="fab-transition">
            <v-card class="text-center text-md-left">
              <v-card-subtitle class="pb-0 text-md-left">Infected</v-card-subtitle>
              <v-card-title id="Infected">{{ cardsData.confirmed.value.toLocaleString() }}</v-card-title>
              <v-card-text>
                <div>{{ new Date(cardsData.lastUpdate).toDateString() }}</div>
              </v-card-text>
            </v-card>
          </v-lazy>
        </v-col>
        <v-col cols="12" md="3">
          <v-lazy min-height="100" transition="fab-transition">
          <v-card class="text-center text-md-left" >
            <v-card-subtitle class="pb-0 text-md-left">Recovered</v-card-subtitle>
            <v-card-title id="Recovered">{{ cardsData.recovered.value.toLocaleString() }}</v-card-title>
            <v-card-text>
              <div>{{ new Date(cardsData.lastUpdate).toDateString() }}</div>
            </v-card-text>
          </v-card>
          </v-lazy>
        </v-col>
        <v-col cols="12" md="3">
          <v-lazy min-height="100" transition="fab-transition">
           <v-card class="text-center text-md-left">
            <v-card-subtitle class="pb-0 text-md-left">Deaths</v-card-subtitle>
            <v-card-title id="Deaths" class="text-center">{{ cardsData.deaths.value.toLocaleString() }}</v-card-title>
            <v-card-text>
              <div>{{ new Date(cardsData.lastUpdate).toDateString() }}</div>
            </v-card-text>
          </v-card>
          </v-lazy>
        </v-col>
      </v-row>
    </div>
  </v-container>
</template>

<script>
export default {
  name: "Cards",
  props: ["cardsData"],
};
</script>

<style scoped>
* {
  font-size: 18px;
}

#Infected {
  color: rgb(58, 99, 212);
}
#Recovered {
  color: rgb(58, 212, 140);
}
#Deaths {
    color: rgb(212, 58, 58);
}

.v-card__title {
  display: inline-flex;
  font-size: 43px;
}

.v-card__subtitle {
  font-size: 18px;
}
</style>
