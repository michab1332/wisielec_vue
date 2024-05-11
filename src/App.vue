<script setup lang="ts">

import Navbar from './components/Navbar.vue';
import { words } from './data.ts';

import { ref } from 'vue';

let imgCount = ref(4);
let currentImg = `/hangman_imgs/${imgCount.value}.png`

</script>

<template>
  <Navbar />
  <div class="container">
    <div class="container__hangmanBox">
      <img :src="currentImg" alt="hangman">
    </div>

  </div>
</template>

<style scoped>
.container {
  background-color: #000;
  height: 90vh;
}

.container__hangmanBox {
  height: 100%;
}

.container__hangmanBox>img {
  height: 99%;

}
</style>
