<script setup>
import { ref, computed, onMounted}  from 'vue'
import song from './assets/song.mp3'
const phrases = [
  "No",
  "Are you sure?",
  "Really sure?",
  "Really, really sure?",
  "Really, really, REALLY sure?",
  "Please don't do this to me",
  "I'm gonna cry ...",
  "You're breaking my heart",
  "Say yes or im taking FIFI",
  "Crispy, click the yes button already!"
]
const count = ref(0)
const messageToShow = computed(() => {
  return phrases[count.value % phrases.length]
})
const valentineName = 'Crispy'
const yesPressed = ref(false)
const loaded = ref(false)
const yesButtonStyle = computed(() => {
  return `font-size: ${count.value * 40 + 16}px`
})

// yes button clicked
const yesClicked = () => {
  yesPressed.value = true;
}

// Function to play the audio
const playAudio = () => {
  const audio = new Audio(song)
  audio.play()
  loaded.value = false
}

onMounted(() => {
  loaded.value = true
})


</script>

<template>
  <div class="valentine-container">
    <template v-if="loaded">
      <h1 class="text-4xl my-4 text-center">I have  very important question for you!</h1>
      <button  class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 rounded" @click="playAudio()">Okay</button>
    </template>
    <template v-if="yesPressed && !loaded">
      <img height="200" alt="bear kiss bear kissing" class="rounded" src="https://tenor.com/view/snoopy-hug-love-gif-15847995.gif"/>
      <h1 class="text-5xl my-4 text-center">Yay!!!!!</h1>
      <h2 class="text-3xl my-4 text-center">Happy Valentine's Day, {{valentineName}}!</h2>
    </template>
    <template v-else-if="!yesPressed && !loaded">
      <img height="200" alt="bear with hearts" class="rounded" src="https://tenor.com/view/happy-valentines-day-love-you-lots-snoopy-and-woodstock-gif-13457459.gif"/>
      <h1 class="text-4xl my-4 text-center">{{valentineName}}, will you be my Valentine?</h1>
      <div class="flex flex-wrap flex-col md:flex-row gap-4 items-center justify-center">
          <button class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 rounded" @click="yesClicked()" :style="yesButtonStyle">Yes</button>
          <button class=" bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded" @click="count++" >{{ messageToShow }}</button>
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
  background-color: #fa5e8d;
}

</style>
