<script setup lang="ts">

import Navbar from './components/Navbar.vue';
import { words } from './data.ts';

import { ref, computed } from 'vue';

let imgCount = ref(1);

const currentImg = computed(() => {
  return `/hangman_imgs/${imgCount.value}.png`;
});

//testfunction
const handleChangeImg = () => {
  imgCount.value = imgCount.value + 1;
}

const randomWord = () => {
  const randomNumber = Math.floor(Math.random() * words.length);
  return words[randomNumber];
}

console.log(randomWord());

</script>

<template>
  <Navbar />
  <div class="container">
    <div class="container__hangmanBox">
      <img @click="handleChangeImg" :src="currentImg" alt="hangman">
    </div>

    <div class="container__actionBox">

    </div>
  </div>
</template>

<style scoped>
.container {
  background-color: #000;
  height: 90vh;
  width: 100%;
  display: flex;
}

.container__hangmanBox {
  height: 100%;
}

.container__hangmanBox>img {
  height: 99%;
}

.container__actionBox {
  width: 100%;
}
</style>
