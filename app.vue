<script setup>
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
    <IconPicker v-if="showIcons" />
    <div id="wrapper" class="bg-light d-flex flex-column align-items-center">
      <div id="form-container" class="col-6 bg-whte p-5 rounded">
        <div class="row">
          <div class="col">
            <div id="demo">
              <iconPicker v-model="icon"></iconPicker>
            </div>
          </div>
        </div>
      </div>
    </div>
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
