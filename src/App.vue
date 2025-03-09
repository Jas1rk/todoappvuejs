<script setup lang="ts">
import { ref } from "vue";
import AddTodo from "./components/AddTodo.vue";
import ListTodo from "./components/ListTodo.vue";

type TaskType = {
  id: number;
  text: string;
};

const tasks = ref<TaskType[]>([]);

const addTask = (task: TaskType) => {
  tasks.value.push(task);
};

const deleteTask = (taskId: number) => {
  tasks.value = tasks.value.filter((task) => task.id !== taskId);
};

const updateTask = (updatedTask:TaskType) => {
   const index = tasks.value.findIndex((task) => task.id === updatedTask.id)
   if(index!==-1){
    tasks.value[index] = updatedTask
   }
}
</script>

<template>
  <AddTodo @add-todo="addTask" />
  <ListTodo :tasks="tasks" @delete-Task="deleteTask"  @updated-Task="updateTask"/>
</template>
