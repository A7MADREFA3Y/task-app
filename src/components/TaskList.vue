<script lang="ts" setup>
import { TransitionGroup } from 'vue';
import type { Task } from '../types';
const props = defineProps<{
    tasks: Task[]
}>();

const emit = defineEmits<{
    toggleDone: [id: string]
    removeTask: [id: string]
}>();

</script>
<template>
    <TransitionGroup name="list" tag="ul" class="task-list">
        <article v-for="task in props.tasks" :key="task.id">
            <label>
                <input @input="emit('toggleDone', task.id)" :checked="task.done" type="checkbox">
                <span :class="{done: task.done}">
                    {{ task.title }}
                </span>
            </label>
            <button @click="emit('removeTask', task.id)" class="outline">
                remove
            </button>
        </article>
    </TransitionGroup>        
</template>

<style>
.task-list{
    margin-top: 1rem;
}

.task{
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.done{
    text-decoration: line-through;
}

.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(300px);
}
</style>