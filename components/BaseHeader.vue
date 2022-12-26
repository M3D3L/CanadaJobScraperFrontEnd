<template>
    <header
      class="header-opacity-100"
    >
      <a href="/">
        <span class="text-4xl top-4 absolute">🍁</span>
      </a>

      <div class="flex md:space-x-4 pr-8 md:pr-0">
        <input
          @input="emitSearch($event.target.value)"
          v-model="search"
          placeholder="Search"
        />
        <button
          @click="emitReset()"
        >
          Reset
        </button>
      </div>
    </header>
</template>

<style lang="css" scoped>
button {
  @apply bg-red-500 hidden md:block w-24 text-white rounded-sm h-9 -mt-1 hover:translate-y-[-2px] hover:bg-red-600 transition-all duration-150 ease-in-out !important;
}

header {
  @apply fixed top-0 flex w-full justify-between bg-gray-900 px-8 text-xl text-white py-6 z-50 opacity-20;
}

input {
  @apply md:w-96 w-32 rounded-sm text-coolgray-500 pb-1 px-4 placeholder-coolgray-500 focus:outline-none focus:ring-2 focus:ring-white focus:ring-opacity-50;
}

.header-opacity-100 {
  @apply opacity-100 h-[5rem];
  transition: opacity 0.2s;
}
</style>

<script>
export default {
  name: 'BaseHeader',
  data() {
    return {
      search: '',
    };
  },
  methods: {
    emitSearch(e) {
      this.$emit('search-results', e);
    },
    emitReset() {
      this.search = '';
      this.$emit('reset');
    },
  },
};
</script>