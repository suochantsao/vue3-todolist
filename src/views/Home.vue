<template>
  <div class="container mx-auto px-4 py-8">
    <h1 class="text-3xl font-bold text-center text-gray-500">
      Vue3 TypeScript ToDoList
    </h1>
    <!-- //* New todo item add area -->
    <ul class="flex justify-center items-center mx-auto mt-8 mb-10">
      <li>
        <input
          type="text"
          class="rounded border-2 border-slate-300 w-60 mr-3 pl-1"
        />
      </li>
      <li>
        <button
          class="rounded-full bg-gray-400 px-3 py-1 text-white hover:bg-pink-300"
        >
          Add
        </button>
      </li>
    </ul>

    <FilterTab :list="tabList" />
    <!-- //* Todo items area// -->
    <div>
      <ul class="flex items-center justify-between py-3 border-b-2">
        <li class="flex">
          <input type="checkbox" name="" id="" class="mx-6" />
          <p>TEST</p>
        </li>
        <li>
          <img class="cursor-pointer mr-6" src="@/assets/img/vector.png" />
        </li>
      </ul>
      <ul class="flex items-center justify-between py-3 border-b-2">
        <li class="flex">
          <input type="checkbox" name="" id="" class="mx-6" />
          <p>TEST</p>
        </li>
        <li>
          <img class="cursor-pointer mr-6" src="@/assets/img/vector.png" />
        </li>
      </ul>
    </div>
    <!-- //* Todo items functional area// -->
    <ul
      class="flex justify-between my-6 py-3 px-4 bg-gray-400 text-white rounded-b-lg"
    >
      <li>0 left</li>
      <li>
        <button class="hover:text-pink-300 font-medium">Clear Completed</button>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import FilterTab from "@/components/FilterTab.vue";
import { defineComponent, ref } from "vue";

export default defineComponent({
  components: {
    FilterTab,
  },
  setup() {
    const tabList = ref<string[]>(["All", "Active", "Complete"]);
    return { tabList };
  },
});
</script>
