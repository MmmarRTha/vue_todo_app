<script setup lang="ts">
import { ref } from 'vue';

const message = ref("TODO APP");
const newTask = ref("");
</script>

<template>
    <main class="max-w-3xl mx-auto my-4 px-4 sm:px-6 lg:px-8">
        <h1 class="text-gray-900 dark:text-white font-bold text-3xl sm:text-4xl lg:text-5xl text-center">
            {{ message }}
        </h1>
        <form class="mt-4 sm:mt-6 lg:mt-8">
            <label class="block mb-2 sm:mb-4 text-gray-200">
                New Task
                <input 
                    name="newTask" 
                    class="mt-2 w-full px-3 py-3 border border-gray-300 rounded-md bg-white dark:bg-gray-800 dark:border-gray-700 dark:text-white focus:outline-none focus:ring-2 focus:ring-cyan-600 text-sm sm:text-base"
                    placeholder="Enter a new task..."
                    v-model="newTask"
                >
            </label>
            <div class="flex justify-end mt-5">
                <button class="bg-cyan-600 hover:bg-cyan-700 text-white font-medium py-2 px-4 rounded-sm transition-colors duration-200 focus:outline-none focus:ring-2 focus:ring-cyan-600 focus:ring-offset-2 w-full sm:w-16">
                    Add
                </button>
            </div>
        </form>
    </main>
</template>
