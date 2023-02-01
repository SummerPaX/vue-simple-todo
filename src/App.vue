<script setup lang="ts">
import { ref } from "vue";
import AddTodo from "./components/AddTodo.vue";
import TodoItem from "./components/TodoItem.vue";
import { v4 as uuidv4 } from "uuid";
import { TodoType } from "./todo.interface";

const todos = ref<TodoType[]>([]);

function todoSubmitted(todo: string) {
	todos.value.push({
		id: uuidv4(),
		todo, // short for todo: todo
	});
}

function toggleDone(todoEntry: TodoType) {
	todos.value = todos.value.filter((item) => item.id !== todoEntry.id);
	if (!todoEntry.done) {
		todos.value.push(todoEntry);
	} else {
		todos.value.unshift(todoEntry);
	}
}
</script>

<template>
	<AddTodo @todoSubmitted="todoSubmitted" />

	<TodoItem
		v-for="todoEntry in todos"
		:key="todoEntry.id"
		:todoItem="todoEntry"
		@deleted="todos = todos.filter((item) => item.id !== todoEntry.id)"
		@toggleDone="toggleDone(todoEntry)"
	></TodoItem>
</template>
