<script setup lang="ts">
import { computed, ref } from 'vue';
import TaskForm from './components/TaskForm.vue';
import type { TaskFilter, Task } from './types';
import TaskList from './components/TaskList.vue';
import FilterButton from './components/FilterButton.vue';
import Footer from './components/Footer.vue';

const meta = {
    title: 'Task Management App',
    description: 'A simple and efficient task management application built with Vue.js',
    keywords: 'task management, todo app, productivity, vue.js',
    author: 'Martha Nieto',
};

document.title = meta.title;

const metaTags = [
    { name: 'description', content: meta.description },
    { name: 'keywords', content: meta.keywords },
    { name: 'author', content: meta.author },
    { property: 'og:title', content: meta.title },
    { property: 'og:description', content: meta.description },
    { property: 'og:type', content: 'website' }
];

metaTags.forEach(tag => {
    const metaTag = document.createElement('meta');
    Object.entries(tag).forEach(([key, value]) => {
        metaTag.setAttribute(key, value);
    });
    document.head.appendChild(metaTag);
});

const message = ref("Task App");
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
    <main class="max-w-3xl mx-auto my-4 px-4 sm:px-6 lg:px-8" role="main">
        <h1 class="text-white font-bold text-3xl sm:text-4xl lg:text-5xl text-center">
            {{ message }}
        </h1>
        <TaskForm @add-task="addTask" />
        <h2 v-if="!tasks.length" class="mt-6 text-xl text-center text-white font-medium">Add a task to get started.</h2>
        <h2 v-else class="mt-6 text-xl text-center text-white font-medium" role="status" aria-live="polite"> {{ totalDone }}/{{ tasks.length }} tasks completed</h2>
        <div v-if="tasks.length" class="flex justify-center sm:justify-end mt-4 gap-6 font-bold" role="tablist" aria-label="Task filters">
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
        <Footer />
    </main>
</template>
