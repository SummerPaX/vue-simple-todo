<script setup lang="ts">
import { ref } from "vue";

const input = ref("");

const emit = defineEmits(["todoSubmitted"]);

function submitTodo() {
	emit("todoSubmitted", input.value);
	input.value = "";
}
</script>

<template>
	<form @submit.prevent="submitTodo">
		<input type="text" v-model="input" placeholder="Add New Todo Item" />
		<button>➕</button>
	</form>
</template>
