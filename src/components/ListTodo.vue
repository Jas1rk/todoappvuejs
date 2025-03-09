<script setup lang="ts">
import { defineProps, defineEmits, reactive } from "vue";

type TaskType = {
  id: number;
  text: string;
};

defineProps<{ tasks: TaskType[] }>();

const emit = defineEmits<{
  (e: "delete-Task", taskId: number): void;
  (e: "updated-Task", task: TaskType): void;
}>();

const editStates = reactive<
  Record<number, { isEditing: boolean; text: string }>
>({});

const editOpen = (task: TaskType) => {
  editStates[task.id] = { isEditing: true, text: task.text };
};

const cancelEdit = (taskId: number) => {
  editStates[taskId].isEditing = false;
};

const saveTask = (taskId: number) => {
  const updated = {
    id: taskId,
    text: editStates[taskId].text,
  };
  emit("updated-Task", updated);
  editStates[taskId].isEditing = false;
};

</script>

<template>
  <div class="flex flex-col justify-center items-center m-auto mt-3">
    <div
      class="flex justify-center items-center gap-16 bg-black p-2 rounded-md mt-2"
      v-for="(todo, index) in tasks"
      :key="todo.id"
    >
      <input
        v-if="editStates[todo.id]?.isEditing"
        type="text"
        class="py-1 px-4 outline-none border border-gray-400 rounded text-white"
        v-model="editStates[todo.id].text"
      />
      <p v-else class="text-white">{{ index + 1 }} = {{ todo.text }}</p>
      <div class="flex gap-3">
        <p v-show="editStates[todo.id]?.isEditing" class="cursor-pointer text-sm" @click="saveTask(todo.id)">✔️</p>
        <p
          v-if="editStates[todo.id]?.isEditing"
          class="cursor-pointer text-sm text-white"
          @click="cancelEdit(todo.id)"
        >
          x
        </p>
        <p v-else class="cursor-pointer text-sm" @click="editOpen(todo)">🖋️</p>
        <p class="cursor-pointer text-sm" @click="emit('delete-Task', todo.id)">
          ❌
        </p>
      </div>
    </div>
  </div>
</template>
