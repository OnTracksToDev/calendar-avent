<script>
import Day from "./Day.vue";

export default {
  components: { Day },
  data() {
    const currentMonth = new Date().getMonth() + 1;
    const currentYear = new Date().getFullYear();
    const daysInMonth = new Date(currentYear, currentMonth, 0).getDate();

    return {
      days: [],
      month: currentMonth, 
      year: currentYear, 
      endDate: daysInMonth, 
    };
  },
  methods: {
    generateCalendar() {
      const daysInMonth = new Date(this.year, this.month, 0).getDate(); // Nombre de jours dans le mois
      const maxDays = Math.min(this.endDate, daysInMonth);

      this.days = Array.from({ length: maxDays }, (_, i) => ({
        number: i + 1,
        content: `Surprise ${i + 1}!`,
        isOpen: false, // État initial fermé
      }));
    },
    resetCalendar() {
      console.log("Réinitialisation du calendrier...");
      this.days.forEach((day) => {
        day.isOpen = false;
      });
    },
    updateEndDate() {
      // Mets à jour endDate au nombre max de jours dans le mois
      this.endDate = new Date(this.year, this.month, 0).getDate();
    },
  },
  watch: {
    // Mets à jour endDate si month ou year change
    month() {
      this.updateEndDate();
    },
    year() {
      this.updateEndDate();
    },
  },
  mounted() {
    this.generateCalendar();
  },
};
</script>

<template>
  <div class="calendar-wrapper">
    <div class="controls mb-4">
      <label>
        Mois:
        <input
          type="number"
          v-model.number="month"
          min="1"
          max="12"
          class="form-control"
          @change="generateCalendar"
        />
      </label>

      <label>
        Année:
        <input
          type="number"
          v-model.number="year"
          min="1900"
          max="2100"
          class="form-control"
          @change="generateCalendar"
        />
      </label>

      <label>
        Jusqu'à (jour max):
        <input
          type="number"
          v-model.number="endDate"
          min="1"
          :max="new Date(year, month, 0).getDate()"
          class="form-control"
          @change="generateCalendar"
        />
      </label>

      <button @click="resetCalendar" class="btn btn-primary mt-2">
        Réinitialiser le calendrier
      </button>
    </div>

    <div class="calendar">
      <Day
        v-for="day in days"
        :key="day.number"
        :number="day.number"
        :content="day.content"
        :is-open="day.isOpen"
        @toggle-open="day.isOpen = !day.isOpen"
      />
    </div>
  </div>
</template>

<style scoped>
.calendar-wrapper {
  max-width: 800px;
  margin: 0 auto;
  text-align: center;
}

.controls {
  display: flex;
  flex-wrap: wrap;
  gap: 15px;
  justify-content: center;
  align-items: center;
}

.controls label {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.calendar {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
  gap: 10px;
  margin: 20px auto;
}
</style>