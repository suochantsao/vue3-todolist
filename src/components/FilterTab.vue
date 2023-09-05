<template>
  <div class="filter-tab">
    <ul
      class="flex justify-center items-center font-medium rounded-t-lg bg-gray-400 text-white"
    >
      <li
        v-for="(item, index) in list"
        :key="index"
        class="w-1/3 text-center hover:bg-pink-300 cursor-pointer rounded-t-lg py-3"
      >
        {{ item }}
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";

@Options({
  props: {
    list: Array,
  },
})
export default class FilterTab extends Vue {
  msg!: string;
}
</script>
