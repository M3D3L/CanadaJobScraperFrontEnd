<template>
    <MetaData />
    <LoadingScreen />
    <BaseHeader ref="header" @search-results="updateSearch($event)" @reset="resetResults()" />
    <JobList :jobs="jobs" :currentPage="currentPage" @update-page="currentPage = $event" @set-observer="resetObservations()" />
    <BaseFooter/>
</template>

<style lang="css">
/* ===== Reset Styles ===== */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* ===== Scrollbar CSS ===== */
/* Firefox */
* {
  scrollbar-width: auto;
  scrollbar-color: #6b7280 #e5e7eb;
  @apply overflow-x-hidden md:overflow-x-visible
}

/* Chrome, Edge, and Safari */
*::-webkit-scrollbar {
  width: 16px;
}

*::-webkit-scrollbar-track {
  background: #e5e7eb;
}

*::-webkit-scrollbar-thumb {
  background-color: #CC3333;
  border-radius: 10px;
  border: 3px solid #ffffff;
}

body {
  @apply bg-coolgray-100 overflow-x-hidden w-full h-screen overflow-y-scroll !important;
}

button {
  @apply text-sm md:bg-red-500 group-hover:translate-y-[-0.5rem] transition-all duration-150 ease-in-out w-40 mx-auto font-bold text-coolgray-500 md:text-white md:shadow-md md:shadow-coolgray-500 mt-2 py-2 rounded-full;
}
</style>

<script>
//import data
import jobsList from "./static/data.json";
//lazy load components
const MetaData = () => import("./components/MetaData.vue");
const BaseHeader = () => import("./components/BaseHeader.vue");
const JobList = () => import("./components/JobList.vue");
const BaseFooter = () => import("./components/BaseFooter.vue");

export default {
  name: "App",
  components: { MetaData, BaseHeader, JobList, BaseFooter },
  data() {
    return {
      jobs: [],
      search: "",
      currentPage: 1,
    };
  },
  beforeMount() {
    this.getData();
  },
  mounted() {

    //sets the header fade in animation on scroll
    const header = document.querySelector("header");
    //header opacity control
    let timeout;

    //ref body using vue ref
    window.addEventListener("scroll", () => {
      // Remove the "header-opacity-100" class from the header
      header.classList.remove("header-opacity-100");

      // Reset the timeout
      clearTimeout(timeout);

      // Set a new timeout to add the "header-opacity-100" class back to the header
      // after 100 milliseconds
      timeout = setTimeout(() => {
        header.classList.add("header-opacity-100");
      }, 100);
    });

    this.resetObservations();
  },
  methods: {
    //Resets the scroll position to the top of the page
    scrollToTop() {
      window.scrollTo({
        top: 0,
      });
    },
    //get the data from the jobs.json file in the root directory
    getData() {
      this.jobs = jobsList;
    },
    setIntersectionObservers() {
      const fadeIn = (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            entry.target.classList.add("fade-in");
          } else {
            entry.target.classList.remove("fade-in");
          }
        });
      };

      const observer = new IntersectionObserver(fadeIn);
      const elements = document.querySelectorAll(".fade-in-element");

      elements.forEach((element) => {
        //if the element is not already in the observer, add it
        if (!observer.observe(element)) {
          observer.observe(element);
        }
      });
    },
    resetObservations() {
      setTimeout(() => {
        this.setIntersectionObservers();
      }, 1000);
      setTimeout(() => {
        this.scrollToTop();
      }, 500);
    },
    resetResults() {
      this.currentPage = 1;
      this.search = "";
      //get the original data
      this.jobs = jobsList;
      this.resetObservations();
    },
    searchResults() {
      this.currentPage = 1;
      this.jobs = jobsList.filter((job) => {
        return (
          job.jobTitle.toLowerCase().includes(this.search.toLowerCase()) ||
          job.business.toLowerCase().includes(this.search.toLowerCase()) ||
          job.location.toLowerCase().includes(this.search.toLowerCase())
        );
      });

      //timout to allow the DOM to update before setting the intersection observer and scrolling to the top
      this.resetObservations()
    },
    updateSearch(search) {
      this.search = search;
      this.searchResults();
    },
  },
};
</script>
