<script setup lang="ts">
import { TodoType } from "../todo.interface";

const props = defineProps<{
	todoItem: TodoType;
}>();

const emit = defineEmits(["toggleDone", "deleted"]);
</script>

<template>
	<div>
		<input
			type="checkbox"
			name="Mark as Done"
			v-model="todoItem.done"
			@click="emit('toggleDone')"
		/>
		<span :class="{ 'line-through opacity-50': todoItem.done }">{{ todoItem.todo }}</span>
		<button @click="emit('deleted')">❌</button>
	</div>
</template>
