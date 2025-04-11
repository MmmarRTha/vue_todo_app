<script setup lang="ts">
import { ref } from 'vue';

const emit = defineEmits<{
    addTask: [newTask: string]
}>();

const newTask = ref("");

function formSubmitted() {
    emit("addTask", newTask.value);
}
</script>

<template>
    <form @submit.prevent="formSubmitted" class="mt-4 sm:mt-6 lg:mt-8">
            <label class="block mb-2 sm:mb-4 text-gray-200">
                New Task
                <input 
                    name="newTask" 
                    class="mt-2 w-full px-3 py-3 border rounded-md bg-gray-800  border-gray-700 text-white focus:outline-none focus:ring-2 focus:ring-cyan-600 text-sm sm:text-base"
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
</template>