<script setup>
import { ref } from 'vue';

const props = defineProps({
  status: {
    type: String,
    default: 'unadmitted'
  },
  number: {
    type: String,
    default: '01'
  }
});

const emit = defineEmits(['update-status']);

const isFlipped = ref(false);

const toggleCard = () => {
  isFlipped.value = !isFlipped.value;
  const newStatus = props.status === 'unadmitted' ? 'admitted' : 'unadmitted';
  emit('update-status', newStatus);
};
</script>

<template>
  <div class="card" @click="toggleCard" :class="{ 'flipped': isFlipped }">
    <div class="content front">
      <div class="number">{{ number }}</div>
      <div class="status">{{ status }}</div>
      <div class="main-action">ПЕРЕВЕНУТЬ</div>
    </div>

    <div class="content back">
      <div class="number">{{ number }}</div>

      <div class="back-content">
        Обратная сторона
      </div>
      <div class="actions">
        <button @click.stop="$emit('answer', true)">✅</button>
        <button @click.stop="$emit('answer', false)">❌</button>

      </div>
    </div>
  </div>
</template>

<style scoped>
.actions {

  display: flex;
  gap: 40px;
  justify-content: center;
  margin-top: 300px;
}

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
  width: calc(100% - 40px);
  height: calc(100% - 40px);
  backface-visibility: hidden;
  border: 1px solid #cce8ff;
  border-radius: 12px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

}

.back {
  transform: rotateY(180deg);

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
  padding: 2px 8px;
  z-index: 1;
  top: -14px;
  left: 15px;
}

.status {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 24px;
  color: #666;
  text-transform: lowercase;
  margin: 0;

}

.main-action {
  font-size: 16px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: #222;
  margin-top: auto;
  text-align: center;
  background-color: #fff;
  padding: 8px;
  border-radius: 4px;
  width: calc(100% - 80px);
  margin-left: auto;
  margin-right: auto;
  margin-bottom: -17px;

}

.back-content {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 20px;
  text-align: center;
}
</style>