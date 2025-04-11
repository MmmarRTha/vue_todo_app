<script setup lang="ts">
import { ref } from 'vue';
import TaskForm from './components/TaskForm.vue';

const message = ref("TODO APP");

function addTask(newTask: string) {
    console.log(newTask)
}
</script>

<template>
    <main class="max-w-3xl mx-auto my-4 px-4 sm:px-6 lg:px-8">
        <h1 class="text-white font-bold text-3xl sm:text-4xl lg:text-5xl text-center">
            {{ message }}
        </h1>
        <TaskForm  @add-task="addTask"/>
    </main>
</template>
