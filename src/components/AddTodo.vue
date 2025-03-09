<script setup lang="ts">
import { ref, watch, defineEmits } from "vue";

const input = ref<string>("");
const errorBar = ref<boolean>(false);

const emit = defineEmits<{
  (e: "add-todo", task: { id: number; text: string }): void;
}>();

const addTodo = () => {
  if (input.value.trim() === "") {
    errorBar.value = true;
    return;
  }
  errorBar.value = false;
  emit("add-todo", {
    id: Date.now(),
    text: input.value,
  });
  input.value = ''
};

watch(input, (newInput) => {
  if (newInput.trim() !== "") {
    errorBar.value = false;
  }
});
</script>

<template>
  <h1 class="text-center font-bold text-2xl mt-3">Todo App</h1>
  <div class="flex flex-col m-auto mt-5 justify-center items-center">
    <div class="flex">
      <input
        type="text"
        placeholder="Add task"
        class="py-1 px-4 outline-none border border-gray-400 rounded"
        :class="errorBar ? 'border-red-500' : 'border-gray-400'"
        v-model="input"
      />

      <button
        class="py-1 px-4 bg-black text-white rounded cursor-pointer"
        @click="addTodo"
      >
        add
      </button>
    </div>
    <p v-show="errorBar" class="text-base text-red-500">
      please enter any task
    </p>
  </div>
</template>
