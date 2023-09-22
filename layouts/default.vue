<template>
  <div>
    <header>
      <Navbar />
    </header>
    <main>
      <slot />
    </main>
    <FooterCustom />
  </div>
</template>

<script setup>
import Navbar from "~/components/navbar.vue";
</script>

<style lang="scss" scoped></style>
