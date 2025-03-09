<script setup lang="ts">
import { ref } from "vue";

const input = ref("");
</script>

<template>
  <h1 class="text-center font-bold text-2xl mt-3">Todo App</h1>
  <div class="flex justify-center items-center m-auto mt-5">
    <input
      type="text"
      placeholder="Add task"
      class="py-1 px-4 outline-none border border-gray-400 rounded"
    />
    <button class="py-1 px-4 bg-black text-white rounded cursor-pointer">
      add
    </button>
  </div>
</template>
