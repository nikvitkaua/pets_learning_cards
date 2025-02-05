<script setup></script>

<template>
  <button>
    <slot></slot>
  </button>
</template>


<style scoped lang="sass">
  button
    border: none
    outline: none
    padding: 20px 40px
    border-radius: 16px
    font-size: 16px
    cursor: pointer
    transition: .4s
    color: #fff
    background: inherit

    &:hover
      opacity: .7

    &:disabled
      color: #ccc
      cursor: not-allowed
      opacity: 0.5

    @media (max-width: 450px)
      padding: 10px 20px
</style>