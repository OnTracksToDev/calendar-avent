<script>
import Day from "./Day.vue";

export default {
  components: { Day },
  data() {
    return {
      days: Array.from({ length: 24 }, (_, i) => ({
        number: i + 1,
        content: `Surprise ${i + 1}!`,
      })),
    };
  },
};
</script>

<template>
  <div class="calendar">
    <Day
      v-for="day in days"
      :key="day.number"
      :number="day.number"
      :content="day.content"
    />
  </div>
</template>

<style scoped>
.calendar {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
  gap: 10px;
  max-width: 600px;
  margin: 0 auto; /* Centre le calendrier horizontalement */
}
</style>
