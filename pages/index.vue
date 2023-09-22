<template>
  <div>
    <section
      id="root"
      class="relative flex min-h-screen flex-col items-center justify-center bg-slate-600"
    >
      <span>this is root</span>
      <button class="rounded-lg bg-slate-600 px-4 py-2 text-white">
        <NuxtLink to="#about"> halo </NuxtLink>
      </button>
    </section>
    <section
      class="relative flex min-h-screen flex-col items-center justify-center"
    >
      <span>this is index</span>
    </section>
    <section
      class="relative flex min-h-screen flex-col items-center justify-center"
    >
      <span>this is index</span>
    </section>
    <section
      class="relative flex min-h-screen flex-col items-center justify-center"
    >
      <span>this is index</span>
    </section>
    <section
      id="about"
      class="relative flex min-h-screen flex-col items-center justify-center"
    >
      <span>this is about</span>
    </section>
  </div>
</template>

<script setup></script>

<style lang="scss" scoped></style>
