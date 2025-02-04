<script setup>
import { ref } from 'vue';

const props = defineProps({
  question: {
    type: Object,
    required: true,
  },
});

const showAnswer = ref(false);

const toggleAnswer = () => {
  showAnswer.value = !showAnswer.value;
};
</script>

<template>
  <div class="card" @click="toggleAnswer">
    <h3 class="card__title">Question #{{ question.id }}</h3>
    <h2 class="card__question">{{ question.question }}</h2>
    <p class="card__answer" v-if="showAnswer">{{ question.answer }}</p>
  </div>
</template>

<style scoped lang="sass">
.card
  position: relative
  background-color: black
  border-radius: 16px
  padding: 20px
  color: #fff
  display: flex
  flex-direction: column
  justify-content: center
  align-items: center
  cursor: grab

  &__title
    position: absolute
    right: 20px
    top: 0

  &__question
    margin-top: 30px
    text-align: center

  &__answer
    text-align: center
    line-height: 1.5em
</style>