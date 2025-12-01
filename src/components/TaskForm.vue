<script setup lang="ts">
import { ref } from "vue"

const emit = defineEmits<{
  addTask: [newTask: string]
}>()

const newTask = ref("")

function formSubmetted() {
  if (newTask.value.trim()) {
    emit("addTask", newTask.value)
    newTask.value = ""  
  }
}
</script>

<template>
  <form @submit.prevent="formSubmetted">
    <label>
      New Task:
      <input v-model="newTask" name="newTask" />
    </label>
    <div class="button-container">
      <button type="submit">Add</button>
    </div>
  </form>
</template>
