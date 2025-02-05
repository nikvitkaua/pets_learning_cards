<script setup>
import { ref } from "vue";

const props = defineProps({
  question: {
    type: Object,
    required: true,
  },
});

const emit = defineEmits(["answer"]);
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
        <div class="card__btns">
          <button class="card__correct" @click="emit('answer', true)">Правильно</button>
          <button class="card__wrong" @click="emit('answer', false)">Неправильно</button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="sass">
.card
  color: #fff
  display: flex
  flex-direction: column
  justify-content: center
  align-items: center
  cursor: grab
  height: 60vh
  width: 100%

  &__inner
    transform-style: preserve-3d
    transition: transform 0.6s
    position: relative
    width: 100%
    height: 100%
    border-radius: 16px
    min-width: 300px

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
    max-width: 700px

  &__answer
    max-width: 700px
    text-align: center
    line-height: 1.5em
    margin-bottom: 40px
    // padding: 0 10px

  &__btns
    display: flex
    justify-content: space-between
    align-items: center
    gap: 30px

    button
      border: none
      outline: none
      padding: 20px 40px
      border-radius: 16px
      font-size: 16px
      cursor: pointer
      transition: .4s
      color: #fff

      &:hover
        opacity: .7

      @media (max-width: 450px)
        padding: 10px 20px

  &__correct
    background: green

  &__wrong
    background: red
    
</style>