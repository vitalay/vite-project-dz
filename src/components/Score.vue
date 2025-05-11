<template>
  <div class="header-score">
    <span class="score-value" aria-live="polite">{{ formattedScore }}</span>
  </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  score: {
    type: Number,
    required: true,

  }
});

const formattedScore = computed(() => {
  return props.score.toString().padStart(3, '0');
});
</script>


<style scoped>
.header-score {
  padding: 8px 16px;
  border-radius: 4px;
  display: inline-flex;
  gap: 8px;
  align-items: center;
}

.score-value {
  color: #007bff;
  font-size: 1.2em;
  font-weight: bold;
  transition: color 0.3s ease;
}
</style>