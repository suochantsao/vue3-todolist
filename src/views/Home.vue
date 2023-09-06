<template>
  <div class="container mx-auto px-4 py-8">
    <h1 class="text-3xl font-bold text-center text-gray-500">
      Vue3 TypeScript ToDoList
    </h1>
    <!-- //* New todo item add area -->
    <ul class="flex justify-center items-center mx-auto mt-8 mb-10">
      <li>
        <input
          v-model="todoValue"
          type="text"
          class="rounded border-2 border-slate-300 w-60 mr-3 pl-1"
          @keypress.enter="AddNewTodo(todoValue)"
        />
      </li>
      <li>
        <button
          class="rounded-full bg-gray-400 px-3 py-1 text-white hover:bg-pink-300"
          @click="AddNewTodo(todoValue)"
        >
          Add
        </button>
      </li>
    </ul>

    <FilterTab :list="tabList" />

    <!-- //* Todo items area// -->
    <div>
      <ul
        class="flex items-center justify-between py-3 border-b-2"
        v-for="item in todoList"
        :key="item.id"
      >
        <li class="flex">
          <input
            type="checkbox"
            name=""
            id=""
            class="mx-6"
            @click="ChangeStatus(item.id)"
          />
          <input
            type="text"
            :class="item.completed ? 'line-through' : ''"
            v-model="item.todo"
          />
        </li>
        <li>
          <img
            class="cursor-pointer mr-6"
            src="@/assets/img/vector.png"
            @click="RemoveTodo(item.id)"
          />
        </li>
      </ul>
    </div>
    <!-- //* Todo items functional area// -->
    <ul
      class="flex justify-between my-6 py-3 px-4 bg-gray-400 text-white rounded-b-lg"
    >
      <li>{{ todoLeft }} left</li>
      <li>
        <button class="hover:text-pink-300 font-medium" @click="leftItemCount">
          Clear Completed
        </button>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import FilterTab from "@/components/filterTab.vue";
import { defineComponent, ref, watch } from "vue";
import Todo from "../types/Todo";
import Tab from "../types/Tab";

export default defineComponent({
  components: {
    FilterTab,
  },
  setup() {
    const tabList = ref<Tab[]>([
      { name: "All", selected: true },
      { name: "Active", selected: false },
      { name: "Completed", selected: false },
    ]);
    const todoList = ref<Todo[]>([
      { id: 0, todo: "討論 Vue 3", completed: false },
    ]);
    const todoValue = ref<string>();
    let todoLeft = ref<number>(1);

    const AddNewTodo = (value: string) => {
      todoList.value.push({
        id: new Date().getTime(),
        todo: value,
        completed: false,
      });
      todoValue.value = "";
    };

    const RemoveTodo = (value: number) => {
      const newTodoList = todoList.value.filter((item) => {
        return item.id !== value;
      });
      todoList.value = newTodoList;
    };

    const ChangeStatus = (value: number) => {
      const selectTodo = todoList.value.find((item) => {
        return item.id === value;
      });
      if (selectTodo) {
        selectTodo.completed = !selectTodo.completed;
      }
      console.log(selectTodo);
    };

    const LeftItemCount = () => {
      const leftItemFilter = todoList.value.filter((item) => {
        return item.completed === false;
      });
      todoLeft.value = leftItemFilter.length;
    };

    watch(
      todoList,
      () => {
        LeftItemCount();
      },
      { deep: true }
    );

    return {
      tabList,
      todoList,
      todoValue,
      todoLeft,
      AddNewTodo,
      RemoveTodo,
      ChangeStatus,
      LeftItemCount,
    };
  },
});
</script>
