<script>
  import { ref, onMounted } from 'vue';
  import { Swiper, SwiperSlide } from 'swiper/vue';
  import Card from './CardComponent.vue';

  import 'swiper/css';

  export default {
    components: {
      Swiper,
      SwiperSlide,
      Card,
    },
    setup() {
      const questions = ref([]);

      onMounted(async () => {
        const response = await fetch('/data/python_dev_junior.json');
        
        const text = await response.text();;

        try {
          const data = JSON.parse(text);
          questions.value = Object.entries(data).map(([id, item]) => ({ id, ...item }));
        } catch (error) {
          console.error('Ошибка парсинга JSON:', error);
        }
      });


      const onSwiper = (swiper) => {};
      const onSlideChange = () => {
        // console.log('slide change');
      };
      return {
        questions,
        onSwiper,
        onSlideChange,
      };
    },
  };
</script>

<template>
  <Swiper
    :slides-per-view="1"
    :space-between="50"
    :loop="true"
    @swiper="onSwiper"
    @slideChange="onSlideChange"
  >
    <SwiperSlide v-for="question in questions" :key="question.id">
      <Card :question="question" />
    </SwiperSlide>
  </Swiper>
</template>

<style scoped>
</style>