<script setup lang="ts">
import TaskForm from './components/TaskForm.vue'
import { ref } from 'vue'

const emit = defineEmits<{ addTask: [task: string] }>()

const message = ref('Welcome to the Task Manager App!')
const newTask = ref('')

function addTask(newTask: string) {
  console.log('Submitting task:',  newTask)
}
</script>

<template>
  <main>
    <h1>{{ message }}</h1>
    <TaskForm @addTask="addTask"/>
  </main>
</template>
