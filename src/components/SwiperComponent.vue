<script setup>
  import { ref } from "vue";
  import { Swiper, SwiperSlide } from 'swiper/vue';
  import Card from './CardComponent.vue';

  import 'swiper/css';

  const props = defineProps({
    questions: Array,
  });

  const emit = defineEmits(["answer"]);

  const swiperInstance = ref(null);

  const onSwiperInit = (swiper) => {
    swiperInstance.value = swiper;
  };

  const handleAnswer = (isCorrect) => {
    emit("answer", isCorrect);

    if (swiperInstance.value) {
      swiperInstance.value.slideNext();
    }
  };
</script>

<template>
  <Swiper
    :slides-per-view="1"
    :space-between="50"
    :loop="true"
    @swiper="onSwiperInit"
    @slideChange="onSlideChange"
  >
    <SwiperSlide v-for="question in questions" :key="question.id">
      <Card :question="question" @answer="handleAnswer" />
    </SwiperSlide>
  </Swiper>
</template>

<style scoped>
</style>