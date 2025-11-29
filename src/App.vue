<script lanng="ts" setup>
import { ref } from "vue"; 
  const message = ref("Tasks App");
  const newTask = ref("");

</script>



<template>
  <main>
    <h1>{{message}}</h1>  
    <from>
    <label>
      New Task:
      <input v-model="newTask" name="newTask"/>
    </label>

    <div class="button-container">
      <button>Add</button>
    </div>
    
    </from>
    <h3>{{newTask}}</h3>
  </main>
</template>

<style scoped>

main {
  max-width: 800px;
  margin: 1rem auto;
}

.button-container {
  display: flex;
  justify-content: end;
}

</style>
