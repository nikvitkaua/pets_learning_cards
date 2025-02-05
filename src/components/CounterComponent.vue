<script setup>
defineProps({
  total: Number,
  remaining: Number,
  correct: Number,
  wrong: Number,
});
</script>

<template>
  <div class="counter">
    <div class="counter__total">Всього питань: {{ total }}</div>
    <div class="counter__left">Залишилось питань: {{ remaining }}</div>
    <div class="counter__correct">Правильно: {{ correct }}</div>
    <div class="counter__wrong">Неправлиьно: {{ wrong }}</div>
  </div>
</template>

<style scoped lang="sass">
.counter
  position: absolute
  top: 0
  right: 0
  background-color: #000
  color: #fff
  padding: 20px
  border-radius: 16px
  max-width: 400px
  display: flex
  flex-direction: column
  gap: 10px

  & > div
    display: flex
    justify-content: space-between
    align-items: center
    gap: 40px

  &__correct
    color: green
  
  &__wrong
    color: red
</style>