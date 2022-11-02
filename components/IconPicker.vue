<script setup>
import { defineEmits, watch, computed, ref } from 'vue';
import iconList from '~/assets/icons.json';

const icons = iconList.icons;
const search = ref('');
const selected = ref('');

const props = defineProps({
  modelValue: String,
});

onBeforeMount(() => {
  search.value = props.modelValue;
});
const emit = defineEmits(['update:modelValue']);
watch(search, (newValue) => {
  emit('update:modelValue', newValue);
});
function select(icon) {
  if (selected.value !== icon.name) {
    selected.value = icon.name;
  } else {
    selected.value = '';
  }
}

const iconsFiltered = computed(() => {
  return icons.filter(
    (i) =>
      i.name.indexOf(search.value.toLowerCase()) !== -1 ||
      i.tags.some((t) => t.indexOf(search.value.toLowerCase()) !== -1)
  );
});
</script>
<template>
  <div class="my-4 rounded bg-transparent border">
    <input
      v-model="search"
      type="text"
      class="block appearance-none w-full py-1 px-2 mb-1 text-base leading-normal bg-transparent rounded border-b active:appearance-none"
      placeholder="Search an icon"
    />
    <Transition name="transition duration-150">
      <div class="h-56 overflow-y-scroll w-80">
        <div
          class="grid grid-cols-6 justify-center items-center"
          v-if="iconsFiltered.length"
        >
          <div v-for="(i, index) in iconsFiltered" :key="index">
            <div
              @click="select(i)"
              class="shadow-sm m-1 p-2 hover:bg-emerald-500 hover:text-white cursor-pointer"
              :class="{ 'bg-emerald-500 text-white': selected == i.name }"
            >
              <Icon :name="`ph:` + i.name" size="24" />
            </div>
          </div>
        </div>
        <div v-else>No results found</div>
      </div>
    </Transition>
  </div>
</template>
