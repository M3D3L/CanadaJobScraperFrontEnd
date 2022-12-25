<template>
  <ul class="fade-in">
    <li v-for="(job, i) in jobs" class="group" :key="job.id">
      <a class="w-full h-full overflow-hidden" :href="job.jobUrl" target="_blank">
        <div class="absolute bottom-4">
          <span class="text-5xl bottom-4 relative z-0">
            🍁
            <span
              class="text-sm w-12 text-white left-2 top-[1.6rem] font-semibold absolute z-10"
            >
              {{ i + 1 }}
            </span>
          </span>
        </div>

        <h2
          class="text-xl md:text-2xl px-2 font-bold capitalize z-50 absolute w-full text-center line-clamp-2"
        >
          {{ job.jobTitle }}
        </h2>
        <h3 class="text-xl font-semibold px-2 line-clamp-1 mt-16">
          {{ job.business }}
        </h3>
        <h4>{{ job.location }}</h4>
        <h4 class="line-clamp-1 px-2">{{ job.salary }}</h4>
        <h4 class="line-clamp-1 px-2">{{ job.howToApply }}</h4>
        <button class="md:mt-10 mt-6">
          View on <br class="md:hidden" />
          Job Bank
        </button>
      </a>
    </li>
  </ul>
</template>

<style lang="css" scoped>
ul {
  @apply grid sm:grid-cols-2 grid-cols-1 md:grid-cols-3 gap-4 md:gap-6 p-4 md:p-8 mt-20 lg:grid-cols-4;
}

li {
  @apply w-full h-72 hover:bg-coolgray-500 hover:text-white border opacity-0 pt-2 border-coolgray-500 transition-all duration-150 shadow-md cursor-pointer shadow-coolgray-500 flex flex-col text-center;
}

.fade-in {
  animation-duration: 0.5s;
  animation-fill-mode: both;
  opacity: 0;
  animation-name: fadeInUp;
}

@keyframes fadeInUp {
  0% {
    opacity: 0;
    transform: translate3d(0, 100%, 0);
  }
  100% {
    opacity: 1;
    transform: none;
  }
}
</style>

<script>
export default {
  props: {
    jobs: {
      type: Array,
      required: true,
    },
  },
};
</script>