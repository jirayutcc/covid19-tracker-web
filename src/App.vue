<template>
  <v-app id="app">
    <v-main class="page-shell">
      <v-container>
        <v-row class="justify-center">
          <v-col cols="12" class="text-center">
            <v-lazy min-height="100" transition="scale-transition">
              <img class="hero-image" src="@/assets/covid19.png" alt="COVID-19 Tracker" />
            </v-lazy>
            <p class="subtitle">Global and country COVID-19 statistics</p>
          </v-col>
        </v-row>

        <v-row class="align-center justify-center mb-4">
          <v-col cols="12" md="6">
            <v-select
              v-model="selectedCountry"
              :items="countryOptions"
              :disabled="loading"
              item-text="label"
              item-value="value"
              label="View"
              outlined
              dense
              hide-details
            />
          </v-col>
          <v-col cols="12" md="2">
            <v-btn block color="primary" :loading="loading" @click="fetchData">
              Refresh
            </v-btn>
          </v-col>
        </v-row>

        <v-alert v-if="error" type="error" prominent>
          {{ error }}
        </v-alert>

        <v-row v-else-if="loading" class="justify-center">
          <v-progress-circular indeterminate color="primary" size="56" />
        </v-row>

        <template v-else>
          <v-row class="justify-center">
            <Cards :cardsData="activeStats" />
          </v-row>

          <v-row class="justify-center">
            <v-col cols="12" md="5">
              <Chart :chartData="activeStats" />
            </v-col>
            <v-col cols="12" md="7">
              <v-card>
                <v-card-title>Top Countries by Cases</v-card-title>
                <v-simple-table>
                  <thead>
                    <tr>
                      <th>Country</th>
                      <th class="text-right">Cases</th>
                      <th class="text-right">Deaths</th>
                      <th class="text-right">Recovered</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="country in topCountries" :key="country.country">
                      <td>{{ country.country }}</td>
                      <td class="text-right">{{ formatNumber(country.cases) }}</td>
                      <td class="text-right">{{ formatNumber(country.deaths) }}</td>
                      <td class="text-right">{{ formatNumber(country.recovered) }}</td>
                    </tr>
                  </tbody>
                </v-simple-table>
              </v-card>
            </v-col>
          </v-row>

          <p class="source-note">
            Source:
            <a href="https://disease.sh/" target="_blank" rel="noopener noreferrer">disease.sh Open Disease API</a>
          </p>
        </template>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import axios from "axios";
import Cards from "@/components/Cards";
import Chart from "@/components/Chart";

const API_BASE_URL = "https://disease.sh/v3/covid-19";

export default {
  name: "App",
  components: {
    Cards,
    Chart
  },
  data() {
    return {
      globalStats: null,
      countries: [],
      selectedCountry: "global",
      loading: false,
      error: "",
    };
  },
  computed: {
    countryOptions() {
      return [
        { label: "Global", value: "global" },
        ...this.countries.map((country) => ({
          label: country.country,
          value: country.country,
        })),
      ];
    },
    activeStats() {
      if (this.selectedCountry === "global") {
        return this.globalStats;
      }

      return this.countries.find((country) => country.country === this.selectedCountry) || this.globalStats;
    },
    topCountries() {
      return this.countries.slice(0, 8);
    },
  },
  created() {
    this.fetchData();
  },
  methods: {
    async fetchData() {
      this.loading = true;
      this.error = "";

      try {
        const [globalResponse, countriesResponse] = await Promise.all([
          axios.get(`${API_BASE_URL}/all`),
          axios.get(`${API_BASE_URL}/countries?sort=cases`),
        ]);

        this.globalStats = globalResponse.data;
        this.countries = countriesResponse.data;
      } catch (e) {
        this.error = "Unable to load COVID-19 data right now. Please try again later.";
      } finally {
        this.loading = false;
      }
    },
    formatNumber(value) {
      return Number(value || 0).toLocaleString();
    },
  },
};
</script>

<style scoped>
* {
  font-family: "Bebas Neue", cursive;
}

.page-shell {
  background: #f5f7fb;
  min-height: 100vh;
  padding-top: 24px;
}

.hero-image {
  max-width: 360px;
  width: 100%;
}

.subtitle {
  color: #5b6472;
  font-size: 22px;
  margin-top: 8px;
}

.source-note {
  color: #5b6472;
  font-size: 16px;
  margin: 18px 0 0;
  text-align: center;
}
</style>
