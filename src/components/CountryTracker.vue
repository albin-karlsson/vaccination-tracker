<template>
  <div>
    <h1 class="text-green-200 font-bold text-2xl">
      {{ name }}
    </h1>
    <div class="w-25 border-4 border-gray-200 bg-gray-100">
      <h3 v-if="global" class="text-gray-500 font-bold text-2xl">
        {{ vaccinationPercent }} %
      </h3>
      <h3 v-else class="text-gray-400 font-bold text-2xl">
        {{ vaccinationPercent }} %
      </h3>
      <div
        v-if="global"
        :style="{ width: vaccinationPercent + '%' }"
        class="h-10 bg-green-400 m-2"
      ></div>
      <div
        v-else
        :style="{ width: vaccinationPercent + '%' }"
        class="h-10 bg-green-200 m-2"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CountryTracker",
  props: ["name", "vaccinated"],
  data() {
    return {
      global: false,
      vaccinationPercent: this.vaccinated,
    };
  },
  created() {
    this.determineGlobal();
    this.formatVaccinationPercent();
  },
  methods: {
    determineGlobal() {
      if (this.name == "Global") {
        this.global = true;
      }
    },
    formatVaccinationPercent() {
      if (
        this.vaccinationPercent > 100
          ? (this.vaccinationPercent = 100)
          : (this.vaccinationPercent = this.vaccinated)
      );
    },
  },
};
</script>
