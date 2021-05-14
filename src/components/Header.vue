<template>
  <header>
    <div class="bg-green-300 p-10 mb-4">
      <i class="fas fa-syringe text-white text-6xl mr-4"></i>
      <h1 class="text-white font-bold text-6xl inline">VaccinationTracker</h1>
      <p class="text-white">
        Updated every day with data from
        <a
          class="hover:text-yellow-400 font-bold"
          href="https://ourworldindata.org/"
          >OurWorldinData.org</a
        >
      </p>
    </div>
  </header>
</template>

<script>
export default {
  name: "Header",
};
</script>
