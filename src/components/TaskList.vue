<script lang="ts" setup>
import type { Task } from '../types';

const props = defineProps<{
    tasks: Task[]
}>();

const emits = defineEmits<{
    toggleDone: [id: string];
    removeTask: [id: string];
}>();
</script>

<template>
    <TransitionGroup name="task-list" tag="div">
        <article v-for="task in props.tasks" :key="task.id"
            class="bg-gray-800 text-white p-5 rounded-md mt-6 flex flex-col sm:flex-row sm:items-center sm:justify-between">
            <label class="flex items-center">
                <input @input="emits('toggleDone', task.id)" :checked="task.done" type="checkbox" class="mr-2">
                <span :class="{ 'line-through text-gray-400': task.done }">{{ task.title }}</span>
            </label>
            <button @click="emits('removeTask', task.id)"
                class="border border-cyan-500 text-cyan-500 hover:border-cyan-300 hover:text-cyan-300 text-base font-medium py-2 px-4 rounded-sm transition-colors duration-200 focus:outline focus:outline-cyan-200 w-full mt-2 sm:mt-0 sm:w-auto hover:shadow-xs shadow-cyan-100">
                Remove
            </button>
        </article>
    </TransitionGroup>
</template>

<style>
.task-list-enter-active,
.task-list-leave-active {
  transition: all 0.5s ease;
}
.task-list-enter-from,
.task-list-leave-to {
  opacity: 0;
  transform: translateX(300px);
}
</style>