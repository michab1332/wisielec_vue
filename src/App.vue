<script setup lang="ts">

import Navbar from '@/components/Navbar.vue';
import { words, letters as l } from './data';

import { ref, computed, type Ref } from 'vue';

const imgCount = ref(1);
const letters = ref(l);

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
const blankGuessedWord = ref(word.split('').map(() => "_"));
const guessedLetters: Ref<string[]> = ref([]);

const guessedWord = computed(() => {
  for (let i = 0; i < word.length; i++) {
    if (guessedLetters.value.includes(word[i])) {
      blankGuessedWord.value[i] = word[i]
    }
  }
  return blankGuessedWord.value;
});

const handleClickOnLetter = (e: any) => {
  const letter: string = e.target.innerText.toLowerCase();
  guessedLetters.value.push(letter);

  //delete letter after click
  if (imgCount.value < 10) {
    letters.value = letters.value.filter(l => l.toLowerCase() !== letter);
  }

  //checking if clicked letter is in word
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
      <div v-if="imgCount < 10" class="container__actionBox__word">
        <span v-for="(letter, index) in guessedWord" :key="index">
          {{ letter }}
        </span>
      </div>
      <div v-else class="container__actionBox__word error">
        GAME OVER
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
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
  align-items: center;
  justify-items: center;
  margin: .5rem;
  gap: .5rem;
}

.container__actionBox__letters__letter {
  padding: 1rem 0;
  cursor: pointer;
  font-weight: 700;
  font-size: 1.2rem;
  border: 5px solid #fff;
  transition: transform .1s ease-in;
  user-select: none;
  width: 60px;
  height: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.container__actionBox__letters__letter:hover {
  transform: translateY(-5%);
}

.error {
  color: red;
}

@media (max-width: 600px) {
  .container__hangmanBox {
    display: none;
  }

  .container__actionBox__letters {
    grid-template-columns: 1fr 1fr 1fr 1fr;
  }
}
</style>
<!--author: Michał Bonowicz -->