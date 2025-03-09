<script setup lang="ts">
import { defineProps, defineEmits } from "vue";

type TaskType = {
  id: number;
  text: string;
};

defineProps<{ tasks: TaskType[] }>();

const emit = defineEmits<{
  (e: "delete-Task", taskId: number): void;
}>();
</script>

<template>
  <div class="flex flex-col justify-center items-center m-auto mt-3">
    <div
      class="flex justify-center items-center gap-16 bg-black p-2 rounded-md mt-2"
      v-for="(todo, index) in tasks"
      :key="todo.id"
    >
      <p class="text-white">{{ index + 1 }} = {{ todo.text }}</p>
      <div class="flex gap-3">
        <p class="cursor-pointer text-sm">🖋️</p>
        <p class="cursor-pointer text-sm" @click="emit('delete-Task', todo.id)">
          ❌
        </p>
      </div>
    </div>
  </div>
</template>
