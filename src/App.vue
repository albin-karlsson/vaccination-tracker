<template>
  <Header />
  <CountryTracker
    name="Global"
    :vaccinated="globalVaccinations"
    :key="componentKey"
  />
  <div class="grid grid-cols-2 gap-4 mt-4">
    <CountryTracker
      :key="country.name"
      v-for="country in countries"
      :name="country.name"
      :vaccinated="country.vaccinated"
    />
  </div>
  <div v-if="loading" class="text-yellow-200 font-bold text-3xl">
    Fetching data...
  </div>
</template>

<script>
import Header from "./components/Header";
import CountryTracker from "./components/CountryTracker";

export default {
  name: "App",
  components: {
    Header,
    CountryTracker,
  },
  data() {
    return {
      countries: [],
      globalVaccinations: 0,
      loading: true,
      componentKey: 0,
    };
  },
  async created() {
    await this.fetchVaccinationData();
  },
  methods: {
    async fetchVaccinationData() {
      const res = await fetch(
        "https://covid.ourworldindata.org/data/owid-covid-data.json"
      );

      const result = await res.json();

      await Object.keys(result).forEach((key) => {
        const data = result[key].data;

        let i;
        for (i = 0; i < 10; i++) {
          const iterationData = result[key].data[data.length - i + 1];

          if (
            typeof iterationData !== "undefined" &&
            typeof iterationData.people_vaccinated_per_hundred !== "undefined"
          ) {
            if (result[key].location === "World") {
              this.globalVaccinations =
                result[key].data[
                  data.length - i + 1
                ].people_vaccinated_per_hundred;
            } else {
              this.countries.push({
                name: result[key].location,
                vaccinated:
                  result[key].data[data.length - i + 1]
                    .people_vaccinated_per_hundred,
              });
            }

            break;
          }
        }
        this.loading = false;
        this.forceRerender();
      });
    },
    forceRerender() {
      this.componentKey += 1;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0px;
}
</style>
