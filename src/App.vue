<script setup lang="ts">
import { computed, ref } from 'vue';
import TaskForm from './components/TaskForm.vue';
import type { TaskFilter, Task } from './types';
import TaskList from './components/TaskList.vue';
import FilterButton from './components/FilterButton.vue';

const message = ref("TODO APP");
const tasks = ref<Task[]>([]);
const filter = ref<TaskFilter>("all");

const totalDone = computed(() => tasks
    .value
    .reduce((total, task) => task.done ? total + 1 : total, 0));

const filteredTasks = computed(() => {
    switch (filter.value) {
        case "all":
            return tasks.value;
        case "todo":
            return tasks.value.filter((task) => !task.done);
        case "done":
            return tasks.value.filter((task) => task.done);
    }
    return tasks.value;
});

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

function removeTask(id: string) {
    const index = tasks.value.findIndex((task) => task.id === id);
    if (index !== -1) {
        tasks.value.splice(index, 1);
    }
}

function setFilter(value: TaskFilter) {
    filter.value = value;
}
</script>

<template>
    <main class="max-w-3xl mx-auto my-4 px-4 sm:px-6 lg:px-8">
        <h1 class="text-white font-bold text-3xl sm:text-4xl lg:text-5xl text-center">
            {{ message }}
        </h1>
        <TaskForm @add-task="addTask" />
        <h3 v-if="!tasks.length" class="mt-6 text-xl text-center text-white font-medium">Add a task to get started.</h3>
        <h3 v-else class="mt-6 text-xl text-center text-white font-medium"> {{ totalDone }}/{{ tasks.length }} tasks completed</h3>
        <div v-if="tasks.length" class="flex justify-center sm:justify-end mt-4 gap-6 font-bold">
            <FilterButton 
                :currentFilter="filter" 
                filter="all" 
                @set-filter="setFilter"
            />
            <FilterButton 
                :currentFilter="filter" 
                filter="todo" 
                @set-filter="setFilter"
            />
            <FilterButton 
                :currentFilter="filter" 
                filter="done" 
                @set-filter="setFilter"
            />
        </div>
        <TaskList :tasks="filteredTasks" @toggle-done="toggleDone" @remove-task="removeTask" />
    </main>
</template>
