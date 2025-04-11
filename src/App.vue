<script setup lang="ts">
import { ref } from 'vue';
import TaskForm from './components/TaskForm.vue';
import type { Task } from './types';
import TaskList from './components/TaskList.vue';

const message = ref("TODO APP");
const tasks = ref<Task[]>([]);

function addTask(newTask: string) {
    tasks.value.push({
        id: crypto.randomUUID(),
        title: newTask,
        done: false,
    });
}

function toggleDone(id: string) {
    const task = tasks.value.find((task) => task.id === id);
    if (task) {
        task.done = !task.done;
    }
}
</script>

<template>
    <main class="max-w-3xl mx-auto my-4 px-4 sm:px-6 lg:px-8">
        <h1 class="text-white font-bold text-3xl sm:text-4xl lg:text-5xl text-center">
            {{ message }}
        </h1>
        <TaskForm  @add-task="addTask"/>
        <h3 class="mt-6 text-xl text-center text-white font-medium" v-if="!tasks.length">Add a task to get started.</h3>
        <h3 class="mt-6 text-xl text-center text-white font-medium" v-else>0 / {{ tasks.length }} tasks completed</h3>
        <TaskList :tasks  @toggle-done="toggleDone" />
    </main>
</template>
