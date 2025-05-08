<template>
  <div class="header-score">
    <span class="score-value">{{ score }}</span>
  </div>
</template>

<script setup>
defineProps({
  score: {
    type: Number,
    required: true
  }
});
</script>

<style scoped>
.header-score {
  padding: 8px 16px;
  border-radius: 4px;
  display: flex;
  gap: 8px;
  align-items: center;
}



.score-value {
  color: #007bff;
  font-size: 1.2em;
}
</style>