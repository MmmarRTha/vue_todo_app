<script lang="ts" setup>
import type { Task } from '../types';

const props = defineProps<{
    tasks: Task[]
}>();

const emits = defineEmits<{
    toggleDone: [id: string]
}>();
</script>

<template>
    <article v-for="task in props.tasks" :key="task.id" class="bg-gray-800 text-white p-5 rounded-md mt-6">
        <label>
            <input
            @input="emits('toggleDone', task.id)" 
            :checked="task.done"
            type="checkbox" 
            class="mr-2" 
            >
            <span :class="{'line-through text-gray-400': task.done}">{{ task.title }}</span>
        </label>
    </article>
</template> 