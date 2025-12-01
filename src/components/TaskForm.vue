<script setup lang="ts">
import { ref } from "vue"

const emit = defineEmits<{
  addTask: [newTask: string]
}>()

const newTask = ref("")
const error = ref("")

function formSubmetted() {
  if (newTask.value.trim()) {
    emit("addTask", newTask.value)
    newTask.value = ""
  }else{
    error.value = "Task title cannot be empty."
  }
}
</script>

<template>
  <form @submit.prevent="formSubmetted">
    <label>
      New Task:
      <input 
      v-model="newTask" 
      name="newTask" 
      :aria-invalid="!!error || undefined"
      @input="error =''"
      />
      <small v-if="error" id="invalid-helper">
        {{ error }}
      </small>
    </label>
    <div class="button-container">
      <button type="submit">Add</button>
    </div>
  </form>
</template>
