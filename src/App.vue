<script setup lang="ts">
import TaskForm from './components/TaskForm.vue'
import { ref } from 'vue'
import type { Task } from './types';

const emit = defineEmits<{ addTask: [task: string] }>()

const message = ref('Welcome to the Task Manager App!')
const tasks = ref<Task[]>([])

function addTask(newTask: string) {
  tasks.value.push({
    id: crypto.randomUUID(),
    title: newTask,
    done: false
  })
}
</script>

<template>
  <main>
    <h1>{{ message }}</h1>
    <TaskForm @addTask="addTask"/>
    <h3> There are {{ tasks.length }} tasks</h3>
  </main>
</template>
