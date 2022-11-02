<script setup>
import { ref } from 'vue';
const showIcons = ref(false);
const icon = ref('');
</script>
<template>
  <div
    class="flex flex-col justify-start items-center w-full h-screen text-black dark:text-white"
  >
    <img src="/logo.png" alt="logo" class="w-20 h-auto mt-5" />
    <ColorPicker class="my-10" />
    <button
      @click="showIcons = !showIcons"
      class="py-2 px-3 border border-black dark:border-white"
    >
      Pick Icon &#8595;
    </button>
    <IconPicker v-if="showIcons" v-model="icon" />
  </div>
</template>
<style>
.light body {
  background: #ffff;
}
.dark body {
  background: rgb(0, 30, 38);
}
</style>
