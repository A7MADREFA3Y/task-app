<script setup lang="ts">
import TaskForm from './components/TaskForm.vue'
import { computed, ref } from 'vue'
import type { Task, TaskFilter } from './types';
import TaskList from './components/TaskList.vue';
import FilterButton from './components/FilterButton.vue';

const emit = defineEmits<{ addTask: [task: string] }>()

const message = ref('Welcome to the Task Manager App!')
const tasks = ref<Task[]>([])
const filter = ref<TaskFilter>("all");

const totalDone = computed(() => tasks
.value
.reduce((total, task) => task.done ? total + 1 : total, 0))

const filteredTasks = computed(() => {
  switch(filter.value){
    case "all":
      return tasks.value;
    
    case"done":
      return tasks.value.filter((task) => task.done)
  
    case"todo":
      return tasks.value.filter((task) => !task.done)
    }
    return tasks.value
})

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

function removeTask(id: string){
  const index = tasks.value.findIndex((task) => task.id === id);
  if (index !== -1){
    tasks.value.splice(index,1)
  }
}

function setFilter(value: TaskFilter) {
  filter.value = value
}

</script>

<template>
  <main>
    <h1>{{ message }}</h1>
    <TaskForm @addTask="addTask"/>
    <h3 v-if="!tasks.length"> Add a Task to Get started.</h3>
    <h3 v-else>{{ totalDone }} / {{ tasks.length }} tasks comleted</h3>
    <div v-if="tasks.length" class="button-container">
      <FilterButton 
        :currentFilter="filter"
        filter="all"
        @set-filter="setFilter"
      />
      <FilterButton
        :currentFilter="filter"
        filter="todo"
        @set-filter="setFilter"
      />
      <FilterButton
        :currentFilter="filter"
        filter="done"
        @set-filter="setFilter"
      />
    </div>
    <TaskList :tasks="filteredTasks" @toggle-done="toggelDone" @removeTask="removeTask"/>
</main>
</template>

<style>

main{
 max-width: 800px;
 margin: 1rem; 
}

.button-container{
  display: flex;
  justify-content: end;
  gap: 0.5rem;
}

</style>

