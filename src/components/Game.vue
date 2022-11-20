<script setup>
import { ref } from '@vue/reactivity';
import { onMounted } from 'vue';

const actualHex = ref('#000000');
const colors = ref(['', '', '']);
const booleanGuess = ref('default');

const makeGuess = (color) => {
  if (color === actualHex.value) {
    booleanGuess.value = 'correct';
    generateRandomHex();
  } else {
    booleanGuess.value = 'incorrect';
  }
};

const generateRandomHex = () => {
  colors.value = colors.value.map((key) => {
    return '#' + Math.floor(Math.random() * 16777215).toString(16);
  });
  const index = Math.floor(Math.random() * colors.value.length);
  actualHex.value = colors.value[index];
};

onMounted(() => {
  generateRandomHex();
});
</script>

<template>
  <div class="game">
    <div>
      <h1>Color Guess</h1>
    </div>
    <div class="newRandomColor" :style="{ backgroundColor: actualHex }"></div>
    <div>
      <p v-if="booleanGuess === 'default'" class="default-state-guess">
        Make yout guess
      </p>
      <p v-else-if="booleanGuess === 'correct'" class="correct-state-guess">
        Correct
      </p>
      <p v-else-if="booleanGuess === 'incorrect'" class="incorrect-state-guess">
        Incorrect
      </p>
    </div>
    <div class="buttons-guess">
      <button
        v-for="(color, idx) in colors"
        :key="idx"
        @click="makeGuess(color)"
        class="guess-button"
      >
        {{ color }}
      </button>
    </div>
  </div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.game {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.newRandomColor {
  width: 300px;
  height: 300px;
  background: #000;
}

.buttons-guess {
  display: flex;
  flex-direction: row;
  padding: 20px 20px;
  width: 300px;
  justify-content: space-around;
}

.guess-button {
  border: none;
  padding: 10px 20px;
  margin: 0 5px;
  transition: opacity 0.15s;
}

.guess-button:hover {
  opacity: 0.75;
}

.guess-button:active {
  opacity: 0.5;
}

.default-state-guess {
  font-weight: bold;
}

.correct-state-guess {
  font-weight: bold;
  color: rgb(13, 96, 13);
}

.incorrect-state-guess {
  font-weight: bold;
  color: rgb(183, 11, 11);
}
</style>
