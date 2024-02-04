<script setup>
import { ref, computed}  from 'vue'
const phrases = [
  "No",
  "Are you sure?",
  "Really sure?",
  "Really, really sure?",
  "Really, really, REALLY sure?",
  "Please don't do this to me",
  "I'm gonna cry ...",
  "You're breaking my heart",
  "No :(",
  "Please say yes",
]
const count = ref(0)
const messageToShow = computed(() => {
  return phrases[count.value % phrases.length]
})
const valentineName = import.meta.env.VITE_VALENTINE_NAME
const yesPressed = ref(false)
const yesButtonStyle = computed(() => {
  return `font-size: ${count.value * 20 + 16}px`
})
</script>

<template>
  <div class="valentine-container">
    <template v-if="yesPressed">
      <img height="200" alt="bear kiss bear kissing" src="https://media.tenor.com/gUiu1zyxfzYAAAAi/bear-kiss-bear-kisses.gif"/>
      <h1 class="text-4xl my-4 text-center">Yay!!!!!</h1>
    </template>
    <template v-else>
      <img height="200" alt="bear with hearts" src="https://gifdb.com/images/high/cute-love-bear-roses-ou7zho5oosxnpo6k.gif"/>
      <h1 class="text-4xl my-4 text-center">{{valentineName}}, will you be my Valentine?</h1>
      <div class="flex flex-wrap flex-col md:flex-row gap-4 items-center justify-center">
          <button class="btn btn-success" @click="yesPressed = true" :style="yesButtonStyle">Yes</button>
          <button class="btn btn-danger" @click="count++" >{{ messageToShow }}</button>
        </div>
      </template>
    </div>
</template>

<style scoped>
.valentine-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  margin-top: 16px;
}

</style>
