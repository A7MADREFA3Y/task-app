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
            </label>
            {{ task.title }}
        </article>
    </div>
</template>

<style>
.task-list{
    margin-top: 1rem;
}
</style>