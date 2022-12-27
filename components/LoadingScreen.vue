<template>
  <div
    v-if="loading"
    class="grid content-center w-full h-screen min-h-screen fixed top-0 left-0 bg-opacity-80 z-[999] overflow-hidden bg-coolgray-100"
  >
    <div class="text-3xl space-y-2 text-coolgray-500 flex flex-col mx-auto text-center">
      <h3>Loading Jobs...</h3>
      <p>{{ emoji }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'LoadingScreen',
  data() {
    return {
      loading: true,
      emojiIndex: 0,
      emojisArray: ['🍁', '🍁🍁', '🍁🍁🍁'],
      emoji: ''
    }
  },
  mounted() {
    //set interval while loading screen is active
    setInterval(() => {
      this.nextEmoji()
    }, 300)
    setTimeout(() => {
      this.loading = false
    }, 1000)
  },
  methods: {
    nextEmoji() {
        // Get the next emoji in the array
        this.emoji = this.emojisArray[this.emojiIndex]
        // If the index is greater than the length of the array, reset it to 0
        if (this.emojiIndex > this.emojisArray.length - 1) {
          this.emojiIndex = 0
        } else {
          // Increment the index
          this.emojiIndex++
        }
      }
  },
}
</script>

<style>
.loading-screen {
  @apply fixed top-0 left-0 right-0 bottom-0 bg-white flex items-center align-middle justify-center;
}
</style>
