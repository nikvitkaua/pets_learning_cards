<script setup>
import { ref } from 'vue';

const props = defineProps({
  question: {
    type: Object,
    required: true,
  },
});

const isFlipped = ref(false);

const toggleCard = () => {
  isFlipped.value = !isFlipped.value;
};
</script>

<template>
  <div class="card" @click="toggleCard">
    <div class="card__inner" :class="{ 'is-flipped': isFlipped }">
      <div class="card__front">
        <h3 class="card__title">Питання #{{ question.id }}</h3>
        <h2 class="card__question">{{ question.question }}</h2>
      </div>
      <div class="card__back">
        <h3 class="card__title">Відповідь</h3>
        <h2 class="card__question">{{ question.question }}</h2>
        <p class="card__answer">{{ question.answer }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped lang="sass">
.card
  padding: 20px
  color: #fff
  display: flex
  flex-direction: column
  justify-content: center
  align-items: center
  cursor: grab
  height: 70vh

  &__inner
    transform-style: preserve-3d
    transition: transform 0.6s
    position: relative
    width: 100%
    height: 100%
    border-radius: 16px

    &.is-flipped
      transform: rotateY(180deg)

  &__front, &__back
    position: absolute
    width: 100%
    height: 100%
    min-height: 200px
    background-color: #000
    border-radius: 16px
    display: flex
    flex-direction: column
    justify-content: center
    align-items: center
    color: #fff
    backface-visibility: hidden
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.3)
  
  &__front
    z-index: 2

  &__back
    transform: rotateY(180deg)

  &__title
    position: absolute
    right: 20px
    top: 0

  &__question
    margin-top: 30px
    text-align: center

  &__answer
    max-width: 700px
    text-align: center
    line-height: 1.5em
</style>