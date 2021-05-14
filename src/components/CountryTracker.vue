<template>
  <div>
    <h1 class="text-green-200 font-bold text-2xl">
      {{ name }}
    </h1>
    <div class="w-25 border-4 border-gray-200 bg-gray-100">
      <h3 class="text-gray-300 font-bold text-2xl">
        {{ vaccinationPercent }} %
      </h3>
      <div
        :style="{ width: vaccinated + '%' }"
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
      vaccinationPercent: this.vaccinated,
    };
  },
  created() {
    this.formatVaccinationPercent();
  },
  methods: {
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
