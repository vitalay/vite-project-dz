<template>
  <div class="card" @click="toggleCard" :class="{ 'flipped': isFlipped }">
    <div class="content front">
      <div class="number">{{ currentNumber }}</div>
      <div class="status">{{ currentStatus }}</div>
      <div class="main-action">ПЕРЕВЕНУТЬ</div>
    </div>

    <div class="content back">
      <div class="back-content">
        Обратная сторона
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const isFlipped = ref(false);
const currentNumber = ref('01');
const currentStatus = ref('unadmitted');
const statuses = ['unadmitted', 'admitted'];

const toggleCard = () => {
  isFlipped.value = !isFlipped.value;

  // Меняем статус
  const currentIndex = statuses.indexOf(currentStatus.value);
  currentStatus.value = statuses[(currentIndex + 1) % statuses.length];
};
</script>

<style scoped>
.card {
  width: 200px;
  height: 300px;
  padding: 20px;
  border-radius: 16px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  position: relative;
  cursor: pointer;
  transition: transform 0.6s;
  transform-style: preserve-3d;
  border: 1px solid #000;
}

.content {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  display: flex;
  flex-direction: column;
  border: 1px solid #cce8ff;
  border-radius: 12px;
  padding: 15px;
}

.back {
  transform: rotateY(180deg);
  background: #f5f5f5;
}

.flipped {
  transform: rotateY(180deg);
}

.number {
  font-size: 18px;
  font-weight: 400;
  color: #222;
  position: absolute;
  background-color: #fff;
  padding: 2px 5px;
  z-index: 1;
}

.status {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 24px;
  color: #666;
  text-transform: lowercase;
}

.main-action {
  font-size: 16px;
  font-weight: 400;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: #222;
  margin-top: auto;
  text-align: center;
  background-color: #fff;
  padding: 5px;
}

.back-content {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 20px;
}
</style>