<script setup lang="ts">

import Navbar from './components/Navbar.vue';
import { words, letters } from './data.ts';

import { ref, computed } from 'vue';

const imgCount = ref(1);

const currentImg = computed(() => {
  if (word === blankGuessedWord.value.join('')) {
    return "/hangman_imgs/win.gif";
  }
  return `/hangman_imgs/${imgCount.value}.png`;
});

//get random word from words array
const randomWord = () => {
  const randomNumber = Math.floor(Math.random() * words.length);
  return words[randomNumber];
}

const word = randomWord();
const blankGuessedWord = ref(word.split('').map(letter => "_"));
const guessedLetters = ref([]);
const guessedWord = computed(() => {
  for (let i = 0; i < word.length; i++) {
    if (guessedLetters.value.includes(word[i])) {
      blankGuessedWord.value[i] = word[i]
    }
  }
  return blankGuessedWord.value;
});

const handleClickOnLetter = (e) => {
  const letter = e.target.innerText.toLowerCase();
  guessedLetters.value.push(letter);
  if (!word.split('').includes(letter)) {
    if (imgCount.value < 10) {
      imgCount.value++;
    }
  }
}

</script>

<template>
  <Navbar />
  <div class="container">
    <div class="container__hangmanBox">
      <img :src="currentImg" alt="hangman">
    </div>

    <div class="container__actionBox">
      <div class="container__actionBox__word">
        <span v-for="(letter, index) in guessedWord" :key="index">
          {{ letter }}
        </span>
      </div>
      <div class="container__actionBox__letters">
        <span @click="handleClickOnLetter" class="container__actionBox__letters__letter"
          v-for="(letter, index) in letters" :key="index">
          {{ letter }}
        </span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  background-color: #000;
  height: 90vh;
  width: 100%;
  display: flex;
  color: #fff;
}

.container__hangmanBox {
  height: 100%;
}

.container__hangmanBox>img {
  height: 99%;
}

.container__actionBox {
  width: 100%;
  display: flex;
  flex-direction: column;
}

.container__actionBox__word {
  border: 2px solid #fff;
  margin: .5rem;
  height: 100%;
  font-size: 5rem;
  display: flex;
  align-items: center;
  justify-content: center;
  user-select: none;
}

.container__actionBox__letters {
  height: 100%;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
  justify-content: center;
  margin: .5rem;
  gap: .5rem;
}

.container__actionBox__letters__letter {
  padding: 1rem 0;
  text-align: center;
  cursor: pointer;
  font-weight: 700;
  font-size: 1.2rem;
  border: 1px solid #fff;
  transition: transform .1s ease-in;
}

.container__actionBox__letters__letter:hover {
  transform: translateY(-5%);
}

@media (max-width: 600px) {
  .container__hangmanBox {
    display: none;
  }
}
</style>
<!--author: Michał Bonowicz -->