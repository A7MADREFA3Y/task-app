<script lang="ts" setup>
import type { Task } from '../types';
const props = defineProps<{
    tasks: Task[]
}>();

const emit = defineEmits<{
    toggleDone: [id: string]
}>();

</script>
<template>
    <div class="task-list">
        <article v-for="task in props.tasks" :key="task.id">
            <label>
                <input @input="emit('toggleDone', task.id)" :checked="task.done" type="checkbox">
                <span :class="{done: task.done}">
                    {{ task.title }}
                </span>
            </label>
            <button>
                remove
            </button>
        </article>
    </div>
    </template>

<style>
.task-list{
    margin-top: 1rem;
}

.done{
    text-decoration: line-through;
}
</style>