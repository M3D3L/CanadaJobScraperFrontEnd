<template>
    <header
      class="fixed top-0 flex w-full justify-between bg-gray-900 px-8 text-xl text-white py-6 z-50 opacity-20"
    >
      <a href="/">
        <span class="text-4xl top-4 absolute">🍁</span>
      </a>

      <div class="flex md:space-x-4 pr-8 md:pr-0">
        <input
          @input="emitSearch($event.target.value)"
          v-model="search"
          placeholder="Search"
          class="md:w-96 w-32 rounded-sm text-coolgray-500 pb-1 px-4 placeholder-coolgray-500"
        />
        <button
          @click="emitReset()"
          class="bg-gray-800 hidden md:block w-24 text-white rounded-sm h-9 -mt-1 hover:translate-y-[-2px] hover:bg-white hover:text-coolgray-500 transition-all duration-150 ease-in-out"
        >
          Reset
        </button>
      </div>
    </header>
</template>

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