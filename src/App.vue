<script setup>
import { defineComponent } from "@vue/runtime-core";

import Game from './components/Game.vue'

defineComponent({
  Game
})
</script>

<template>
  <Game></Game>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>
