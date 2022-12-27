<template>
    <footer class="bg-gray-800 text-gray-100 py-4 fixed w-full bottom-0 z-100">
      <div class="container mx-auto flex items-center justify-between px-4">
        <p class="text-xs font-medium">{{date}} Guillermo Medel</p>
        <a href="https://guillermomedel.com" class="font-bold text-xs hover:text-gray-400"
          >Visit GuillermoMedel.com</a
        >
      </div>
    </footer>
</template>

<script>
export default {
 name: "BaseFooter",
 data() {
   return {
    date: new Date().getFullYear()
   };
 },
};
</script>