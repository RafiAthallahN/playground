<template>
  <div>
    <nav
      class="fixed left-0 right-0 top-0 z-50 bg-opacity-60 px-6 py-4 drop-shadow-sm backdrop-blur"
    >
      <div class="container mx-auto flex items-center justify-between">
        <span>halo</span>
        <ul class="flex flex-row gap-4 text-white">
          <li v-for="(link, index) in page" :key="index" class="">
            <NuxtLink :to="link.url">{{ link.title }}</NuxtLink>
          </li>
        </ul>
      </div>
    </nav>
  </div>
</template>

<script setup>
const page = [
  {
    title: "Home",
    url: "/",
  },
  {
    title: "About",
    url: "/about",
  },
];
</script>

<style lang="scss" scoped></style>
