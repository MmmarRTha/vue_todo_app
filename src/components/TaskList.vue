<script lang="ts" setup>
import type { Task } from '../types';

const props = defineProps<{
    tasks: Task[]
}>();
</script>

<template>
    <article v-for="task in props.tasks" :key="task.id" class="bg-gray-800 text-white p-5 rounded-md mt-6">
        {{ task.title }}
    </article>
</template> 