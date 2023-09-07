<template>
  <div class="filter-tab">
    <ul
      class="flex justify-center items-center font-medium rounded-t-lg bg-gray-400 text-white"
    >
      <li
        v-for="(item, index) in list"
        :key="index"
        :class="item.selected ? 'bg-pink-300' : 'bg-gray-400'"
        class="w-1/3 text-center hover:bg-pink-300 cursor-pointer rounded-t-lg py-3"
        @click="console.log(item)"
      >
        {{ item.name }}
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";

export default defineComponent({
  props: {
    list: Array,
  },
  setup() {
    const currentTab = ref<string>("");
  },
});
</script>
