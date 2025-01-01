<script>
import Calendar from "./components/Calendar.vue";

export default {
  components: { Calendar },
};
</script>


<template>
  <div id="app" class="container py-4">
    <!-- Titre principal -->
    <header class="text-center mb-4">
      <h1 class="display-4 text-primary">Calendrier de l'Avent</h1>
    </header>

    <!-- Tableau du calendrier -->
    <main class="text-center">
      <Calendar />
    </main>
  </div>
</template>

<style>
</style>
