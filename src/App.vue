<template>
  <div class="app-container">
    <header class="header app-header">
      <h1 class="title">Запомни слово</h1>
      <div class="header-controls">
        <Score :score="currentScore" />
        <button class="btn-icon" @click="handleIconClick" aria-label="Локация">
          <IconLocation color="#008BFE" :size="28" class="icon-class" />
        </button>
      </div>
    </header>

    <main class="main-content">
      <Card v-if="isGameStarted" :status="cardStatus" @update-status="handleStatusUpdate" @answer="handleAnswer" />
      <button class="btn" @click="startGame" :disabled="isGameStarted">
        {{ isGameStarted ? 'Игра начата' : 'Начать игру' }}
      </button>
    </main>
  </div>
</template>


<script setup>
import { ref } from 'vue';
import Card from "./components/Card.vue";
import Score from './components/Score.vue';
import IconLocation from "./icons/IconLocation.vue";

// Состояния приложения
const currentScore = ref(100);
const cardStatus = ref('unadmitted');
const isGameStarted = ref(false);

// Обработчики событий карточки
const handleStatusUpdate = (newStatus) => {
  cardStatus.value = newStatus;
};

const handleAnswer = (isCorrect) => {
  currentScore.value += isCorrect ? 1 : -1;
};

// Запуск игры
const startGame = () => {
  isGameStarted.value = true;
  currentScore.value = 0;
  cardStatus.value = 'unadmitted';
};

// Клик по иконке локации
const handleIconClick = () => {
  console.log('Нажатие на иконку локации');
};
</script>


<style scoped>
.app-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  background: white;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 16px 24px;
}

.main-content {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: calc(100vh - 80px);
  padding: 20px;
}

.btn {
  background: var(--color-bg);
  color: var(--color-cl);
  width: 335px;
  height: 68px;
  border-radius: 100px;
  font-size: 24px;
  border: none;
  cursor: pointer;
  font-weight: 400;
  transition: transform 0.2s;
  margin: 0 20px;

}

.btn:hover {
  transform: scale(1.02);
}

.title {
  font-family: var(--font);
  font-weight: 700;
  font-size: 16px;
  line-height: 150%;
  letter-spacing: 0.12em;
  color: #222;
  margin: 0;
}

.btn-start {
  border: none;
  border-radius: 36px;
  padding: 12px 24px;
  height: 48px;
  box-shadow: 0 0 4px 0 rgba(0, 0, 0, 0.15);
  background: #cce8ff;
  display: flex;
  align-items: center;
  gap: 8px;
}
</style>