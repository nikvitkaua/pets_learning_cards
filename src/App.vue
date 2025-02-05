<script setup>
import { ref, onMounted, watch } from "vue";
import Swiper from "./components/SwiperComponent.vue";
import Counter from "./components/CounterComponent.vue";
import InterviewSelectionPopup from "./components/InterviewSelectionPopup.vue";

const questions = ref([]);
const currentIndex = ref(0);
const correctCount = ref(0);
const wrongCount = ref(0);
const filePath = ref('');
const showPopup = ref(true);



onMounted(() => {
  if (sessionStorage.getItem('interviewData')) {
    const savedData = JSON.parse(sessionStorage.getItem('interviewData'));
    const { language, position } = savedData;

    if (language && position) {
      showPopup.value = false;

      if (language === 'Python' && position === 'Junior') {
        filePath.value = '/data/python_dev_junior.json';
      }
    }
  }
});


watch(filePath, async (newFilePath) => {
  if (!newFilePath) return;

  try {
    const response = await fetch(newFilePath);
    const text = await response.text();
    const data = JSON.parse(text);

    const parsedQuestions = Object.entries(data).map(([id, item]) => ({ id, ...item }));

    shuffleArray(parsedQuestions);
    questions.value = parsedQuestions;
  } catch (error) {
    console.error("Помилка парсингу JSON:", error);
  }
});

const setFilePath = (path) => {
  filePath.value = path;
};

const shuffleArray = (array) => {
  for (let i = array.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [array[i], array[j]] = [array[j], array[i]];
  }
};

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
  <InterviewSelectionPopup 
    v-if="showPopup" 
    @setFilePath="setFilePath"
    @close="showPopup = false"
  />


  <div v-else class="container">
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
