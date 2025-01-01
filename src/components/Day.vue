<script>
export default {
  props: {
    number: Number,
    content: String,
  },
  data() {
    return {
      isOpen: false,
    };
  },
  methods: {
    openDay() {
      this.isOpen = true;
    },
  },
};
</script>

<template>
  <div
    class="day card text-center"
    :class="{ 'bg-light': !isOpen, 'bg-warning': isOpen }"
    @click="openDay"
  >
    <div v-if="isOpen" class="card-body p-3">
      <p class="card-text">{{ content }}</p>
    </div>
    <div v-else class="card-body p-3">
      <h5 class="card-title">{{ number }}</h5>
    </div>
  </div>
</template>

<style scoped>
.day {
  width: 100px;
  height: 100px;
  cursor: pointer;
  margin: 5px;
  transition: transform 0.3s ease-in-out;
}
.day:hover {
  transform: scale(1.05);
}
</style>
