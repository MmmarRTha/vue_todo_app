<script setup lang="ts">
import { ref } from 'vue';

const emit = defineEmits<{
    addTask: [newTask: string]
}>();

const newTask = ref("");
const error = ref("");

function formSubmitted() {
    if (newTask.value.trim()) {
        emit("addTask", newTask.value.trim());
        newTask.value = "";
    } else {
        error.value = "Task cannot be empty!";
    }
}
</script>

<template>
    <form @submit.prevent="formSubmitted" class="mt-4 sm:mt-6 lg:mt-8" role="form">
        <label for="newTask" class="block text-white text-md font-semibold">
            New Task
        </label>
        <input 
            id="newTask"
            name="newTask" 
            class="mt-2 w-full px-3 py-3 border rounded-md bg-gray-800 border-gray-700 text-white focus:outline-none focus:ring-2 focus:ring-cyan-600 text-sm sm:text-base"
            :class="{'border-red-400 focus:ring-red-400': error}"
            placeholder="Enter a new task..."
            v-model="newTask"
            @input="error = ''"
            :aria-invalid="!!error"
            :aria-describedby="error ? 'error-message' : undefined"
        />
        <small 
            id="error-message"
            class="text-red-500 block mt-2 font-bold"
            v-if="error"
            role="alert"
        >
            {{ error }}
        </small>
        <div class="flex justify-end mt-5">
            <button 
                type="submit"
                class="bg-cyan-600 hover:bg-cyan-700 text-white font-medium py-2 px-4 rounded-sm transition-colors duration-200 focus:outline-none focus:ring-2 focus:ring-cyan-600 focus:ring-offset-2 w-full sm:w-16"
            >
                Add
            </button>
        </div>
    </form>
</template>