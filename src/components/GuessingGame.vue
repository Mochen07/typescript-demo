<template>
  <div>
    <h1>猜数字</h1>
    <p>猜一个数字在0到100之间</p>
    <input type="number" v-model.number="guess" @keyup.enter="checkGuess" />
    <button @click="checkGuess">推测</button>
    <p>{{ result }}</p>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue"

export default defineComponent({
  name: "GuessTheGame",
  setup() {
    const randomNumber = Math.floor(Math.random() * 100)
    const guess = ref(0)
    const guesses = ref(0)
    const result = ref('')

    const checkGuess = () => {
      if (guess.value === randomNumber) {
        result.value = `恭喜！你在${ guesses.value }次猜测中猜出了这个数字。`
      } else if (guess.value < randomNumber) {
        result.value = `太低了，再猜一遍。`
        guesses.value++
      } else {
        result.value = `太高了，再猜一遍。`
        guesses.value++
      }
    }

    return {
      guess,
      result,
      checkGuess
    }
  }
})
</script>