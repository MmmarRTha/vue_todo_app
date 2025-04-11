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
    <article v-for="task in props.tasks" :key="task.id"
        class="bg-gray-800 text-white p-5 rounded-md mt-6 flex flex-col sm:flex-row sm:items-center sm:justify-between">
        <label class="flex items-center">
            <input @input="emits('toggleDone', task.id)" :checked="task.done" type="checkbox" class="mr-2">
            <span :class="{ 'line-through text-gray-400': task.done }">{{ task.title }}</span>
        </label>
        <button
            class="bg-cyan-600 hover:bg-cyan-700 text-white text-base font-medium py-2 px-4 rounded-sm transition-colors duration-200 focus:outline-none focus:ring-2 focus:ring-cyan-600 focus:ring-offset-2 w-full mt-2 sm:mt-0 sm:w-auto">
            Remove
        </button>
    </article>
</template>