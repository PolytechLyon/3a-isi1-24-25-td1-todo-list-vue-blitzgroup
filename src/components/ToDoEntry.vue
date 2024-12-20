<script setup>
	const props = defineProps(['Titre', 'Index']);
</script>

<template>
	<li>
		<span>
			{{ Titre }}
		</span>
		<button @click="$emit('edit-todo', Index)">Edit</button>
		<button @click="$emit('rm-todo', Titre)">Delete</button>
	</li>
</template>

<style scoped>
span {
	display: inline-block;
	width: 15em;
}
button {
	margin: 0.2em;
}
</style>