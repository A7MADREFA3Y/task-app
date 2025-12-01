<script setup lang="ts">
import TaskForm from './components/TaskForm.vue'
import { ref } from 'vue'
import type { Task } from './types';
import TaskList from './components/TaskList.vue';

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

function toggelDone(id: string){
  const task = tasks.value.find((task) => task.id === id);
  if(task) { 
    task.done = !task.done
  }
}

</script>

<template>
  <main>
    <h1>{{ message }}</h1>
    <TaskForm @addTask="addTask"/>
    <h3 v-if="!tasks.length"> Add a Task to Get started.</h3>
    <h3 v-else>0 / {{ tasks.length }} tasks comleted</h3>
    <TaskList :tasks @toggle-done="toggelDone"/>
</main>
</template>
