<script setup lang="ts">
import { ref } from 'vue';
import TaskForm from './components/TaskForm.vue';
import type { Task } from './types';

const message = ref("TODO APP");
const tasks = ref<Task[]>([]);

function addTask(newTask: string) {
    tasks.value.push({
        id: crypto.randomUUID(),
        title: newTask,
        done: false,
    });
}
</script>

<template>
    <main class="max-w-3xl mx-auto my-4 px-4 sm:px-6 lg:px-8">
        <h1 class="text-white font-bold text-3xl sm:text-4xl lg:text-5xl text-center">
            {{ message }}
        </h1>
        <TaskForm  @add-task="addTask"/>
        <h3 class="mt-6 text-xl text-center text-white font-medium">There are {{ tasks.length }} tasks.</h3>
    </main>
</template>
