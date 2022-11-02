<script setup>
import { defineEmits, watch, computed, ref } from 'vue';
import iconList from '~/assets/icons.json';

const icons = iconList.icons;
const hoverPanel = ref(false);
const search = ref('');
const beforeSelect = ref('');
const selected = ref('');
const timeout = ref(undefined);
const picker = ref(null);

/* onBeforeMount(() => {
  search.value = modelValue;
}); */

/* watch(search, (newValue) => {
  search.value= newValue;
}); */
/* function blur() {
  timeout.value = setTimeout(() => {
    focusOn.value = false;
  }, 150);
}
function focus() {
  focusOn.value = true;
} */
function select(icon) {
  clearTimeout(timeout);
  if (icon) {
    if (search.value != selected.value) beforeSelect.value = search.value;
    selected.value = icon.title;
    search.value = icon.title;
  }
  picker.focus();
}
const iconsFiltered = computed(() => {
  return icons.filter(
    (i) =>
      i.name.indexOf(search.value) !== -1 ||
      i.tags.some((t) => t.indexOf(search.value) !== -1)
  );
});
</script>
<template>
  <div class="my-4">
    <input
      v-model="search"
      @blur="blur"
      @focus="focus"
      type="text"
      class="block appearance-none w-full py-1 px-2 mb-1 text-base leading-normal bg-white text-grey-darker border border-grey rounded"
      placeholder="Search an icon"
    />
    <Transition name="icon-preview-fade">
      <div class="bg-slate-300 h-56 overflow-y-scroll">
        <div
          @click="select(undefined)"
          @mouseover="hoverPanel = true"
          @mouseout="hoverPanel = false"
          class="grid grid-cols-6 justify-center items-center rounded-lg"
          :class="[{ 'shadow-sm': !hoverPanel }, { 'shadow-lg': hoverPanel }]"
        >
          <div
            v-for="(i, index) in iconsFiltered"
            :key="index"
            class="icon-preview"
          >
            <div
              @click.prevent.stop="select(i)"
              :class="[
                'icon-wrapper',
                'rounded',
                'shadow-sm',
                { selected: i.name == selected },
              ]"
            >
              <Icon :name="`ph:` + i.name" size="24" />
            </div>
          </div>
        </div>
      </div>
    </Transition>
  </div>
</template>
