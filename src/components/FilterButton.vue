<script lang="ts" setup>
import type { TaskFilter } from '../types';
import { computed } from 'vue';

const props = defineProps<{
    filter: TaskFilter;
    currentFilter: TaskFilter;
}>();

const emits = defineEmits<{
    setFilter: [filter: TaskFilter];
}>();

const getButtonClasses = computed(() => {
    const baseClasses = "px-4 py-2 rounded capitalize transition-colors duration-200 text-white";
    
    if (props.currentFilter === props.filter) {
        switch (props.filter) {
            case "all":
                return `${baseClasses} bg-cyan-400 font-medium`;
            case "todo":
                return `${baseClasses} bg-fuchsia-400`;
            case "done":
                return `${baseClasses} bg-teal-500`;
        }
    }
    
    return `${baseClasses} font-normal bg-slate-500`;
});
</script>

<template>
    <button
        :class="getButtonClasses"
        @click="emits('setFilter', props.filter)">
        {{ props.filter }}
    </button>
</template>