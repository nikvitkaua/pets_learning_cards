<script setup>
import { ref, defineEmits } from 'vue';
import ButtonComponent from './elements/ButtonComponent.vue';

const selectedLanguage = ref(null);
const selectedPosition = ref(null);
const selectedFramework = ref(null);

const emit = defineEmits();

const selectLanguage = (language) => {
  selectedLanguage.value = language;
};

const selectPosition = (position) => {
  selectedPosition.value = position;
};

const selectFramework = (framework) => {
  selectedFramework.value = framework;
};

const startInterview = () => {
  let filePath = '';

  if (selectedLanguage.value === 'Python' && selectedPosition.value === 'Junior') {
    filePath = '/data/python_dev_junior.json';
  } else if (selectedLanguage.value === 'JavaScript' && selectedPosition.value === 'Junior' && selectedFramework.value === 'Vue') {
    filePath = '/data/js_vue_junior.json';
  } else {
    console.log('Cant find the file')
  }

  emit('setFilePath', filePath);

  sessionStorage.setItem('interviewData', JSON.stringify({
    language: selectedLanguage.value,
    position: selectedPosition.value,
    framework: selectedFramework.value,
  }));

  emit('close');
};
</script>

<template>
  <div class="modal">
    <div class="modal-content">
      <h2>Оберіть параметри для співбесіди</h2>

      <div v-if="!selectedLanguage">
        <h3>Оберіть мову програмування або направлення</h3>
        <ButtonComponent @click="selectLanguage('Python')">Python</ButtonComponent>
        <ButtonComponent @click="selectLanguage('JavaScript')">JavaScript</ButtonComponent>
      </div>

      <div v-if="selectedLanguage && !selectedPosition">
        <h3>Оберіть бажану позицію</h3>
        <ButtonComponent @click="selectPosition('Junior')">Junior</ButtonComponent>
        <ButtonComponent disabled @click="selectPosition('Middle')">Middle</ButtonComponent>
        <ButtonComponent disabled @click="selectPosition('Senior')">Senior</ButtonComponent>
      </div>

      <div v-if="selectedPosition && selectedLanguage === 'JavaScript' && !selectedFramework">
        <h3>Оберіть фреймворк</h3>
        <ButtonComponent disabled @click="selectFramework('React')">React</ButtonComponent>
        <ButtonComponent @click="selectFramework('Vue')">Vue</ButtonComponent>
        <ButtonComponent disabled @click="selectFramework('Angular')">Angular</ButtonComponent>
      </div>

      <ButtonComponent v-if="selectedFramework || selectedPosition" @click="startInterview">Перейти до питань</ButtonComponent>
      <ButtonComponent v-if="!selectedLanguage" @click="emit('close')">Закрити</ButtonComponent>
    </div>
  </div>
</template>

<style scoped lang="sass">
.modal 
  position: fixed
  top: 0
  left: 0
  width: 100%
  height: 100%
  display: flex
  justify-content: center
  align-items: center
  background-color: rgba(0, 0, 0, 0.5)


.modal-content 
  background-color: #000
  color: #fff
  padding: 20px
  text-align: center
  border-radius: 10px

</style>
