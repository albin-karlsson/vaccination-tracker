<template>
  <Header />
  <div class="grid grid-cols-2 gap-4">
    <CountryTracker
      :key="country.name"
      v-for="country in countries"
      :name="country.name"
      :vaccinated="country.vaccinated"
    />
  </div>
</template>

<script>
import Header from "./components/Header";
import CountryTracker from "./components/CountryTracker";
//import CountrySelector from "./components/CountrySelector";

export default {
  name: "App",
  components: {
    Header,
    CountryTracker,
  },
  data() {
    return {
      countries: [],
    };
  },
  created() {
    this.fetchVaccinationData();
  },
  methods: {
    async fetchVaccinationData() {
      const res = await fetch(
        "https://covid.ourworldindata.org/data/owid-covid-data.json"
      );

      const result = await res.json();

      Object.keys(result).forEach((key) => {
        const data = result[key].data;

        let i;
        for (i = 0; i < 10; i++) {
          const iterationData = result[key].data[data.length - i + 1];

          if (
            typeof iterationData !== "undefined" &&
            typeof iterationData.people_vaccinated_per_hundred !== "undefined"
          ) {
            this.countries.push({
              name: result[key].location,
              vaccinated:
                result[key].data[data.length - i + 1]
                  .people_vaccinated_per_hundred,
            });
            break;
          }
        }
      });
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
