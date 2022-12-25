<template>
    <MetaData />
    <BaseHeader @search-results="updateSearch($event)" @reset="resetResults()" />
    <JobList :jobs="jobs" />
    <BaseFooter v-if="footer && jobs.length > 4" :date="date" />
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
}

/* Chrome, Edge, and Safari */
*::-webkit-scrollbar {
  width: 16px;
}

*::-webkit-scrollbar-track {
  background: #e5e7eb;
}

*::-webkit-scrollbar-thumb {
  background-color: #6b7280;
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
      backup: [],
      date: new Date().getFullYear(),
      footer: false
    };
  },
  beforeMount() {
    this.getData();
  },
  mounted() {
    //set the backup array to the jobs array for filtering and resetting our results
    this.backup = this.jobs;

    //set the intersection observers for the fade in animation
    this.setIntersectionObservers();
    
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

    setTimeout(() => {
      this.scrollToTop();
    }, 1250);
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
      for (let i = 0; i < jobsList.length; i++) {
        this.jobs.push(jobsList[i]);
      }
    },
    setIntersectionObservers() {
      this.footer = false;
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
      const elements = document.querySelectorAll("li");

      elements.forEach((element) => {
        //if the element is not already in the observer, add it
        if (!observer.observe(element)) {
          observer.observe(element);
        }
      });
      this.footer = true;
    },
    resetResults() {
      this.search = "";
      this.jobs = this.backup;
      setTimeout(() => {
        this.setIntersectionObservers();
      }, 1000);
      setTimeout(() => {
        this.scrollToTop();
      }, 1500);
    },
    searchResults() {
      this.jobs = this.backup.filter((job) => {
        return (
          job.jobTitle.toLowerCase().includes(this.search.toLowerCase()) ||
          job.business.toLowerCase().includes(this.search.toLowerCase()) ||
          job.location.toLowerCase().includes(this.search.toLowerCase())
        );
      });

      //timout to allow the DOM to update before setting the intersection observer and scrolling to the top
      setTimeout(() => {
        this.setIntersectionObservers();
      }, 1000);
      setTimeout(() => {
        this.scrollToTop();
      }, 1500);
    },
    updateSearch(search) {
      this.search = search;
      this.searchResults();
    },
  },
};
</script>
