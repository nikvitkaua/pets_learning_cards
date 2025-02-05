<script setup>
import { ref, onMounted } from "vue";
import Swiper from "./components/SwiperComponent.vue";
import Counter from "./components/CounterComponent.vue";

const questions = ref([]);
const currentIndex = ref(0);
const correctCount = ref(0);
const wrongCount = ref(0);

const shuffleArray = (array) => {
  for (let i = array.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [array[i], array[j]] = [array[j], array[i]];
  }
};

onMounted(async () => {
  try {
    const response = await fetch("/data/python_dev_junior.json");
    const text = await response.text();
    const data = JSON.parse(text);

    const parsedQuestions = Object.entries(data).map(([id, item]) => ({ id, ...item }));

    shuffleArray(parsedQuestions);
    questions.value = parsedQuestions;
  } catch (error) {
    console.error("Ошибка парсинга JSON:", error);
  }
});

const handleAnswer = (isCorrect) => {
  if (isCorrect) {
    correctCount.value++;
  } else {
    wrongCount.value++;
  }
  if (currentIndex.value < questions.value.length - 1) {
    currentIndex.value++;
  }
};
</script>

<template>
  <div class="container">
    <Counter 
      :total="questions.length"
      :remaining="questions.length - currentIndex"
      :correct="correctCount"
      :wrong="wrongCount"
    />
    <Swiper :questions="questions" @answer="handleAnswer" />
  </div>
</template>

<style scoped>
</style>
