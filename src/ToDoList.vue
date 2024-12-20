<script setup>

import { ref } from 'vue';
import ToDoEntry from './components/ToDoEntry.vue';

let titres = ref(["oui", "non", "peut-être"]);
let editMode = ref(false);
let currentEditIndex = ref(0);

function ajouterTodo() {
	const newTodo = document.getElementById("new-todo-item-title").value;
	titres.value.push(newTodo);
}

function editTodo(todoIndex) {
	editMode.value = true;
	currentEditIndex.value = todoIndex;
}

function deleteTodo(title) {
	// moche mais parfaitement fonctionnel
	titres.value = titres.value.filter((tt) => {return title != tt});
}

function confirmEdit() {
	const newTitle = document.getElementById("edit-todo-item-title").value;
	titres.value[currentEditIndex.value] = newTitle;
}

</script>

<template>
	<h2>Todo List</h2>
	<ol id="todo-list">
		<ToDoEntry v-for="(titre, index) in titres" :Titre="titre" :Index="index" @edit-todo="editTodo" @rm-todo="deleteTodo"/>
	</ol>
	<div id="new-item" :hidden="editMode">
		<h3>New todo item</h3>
		<label for="new-todo-item-title">Title</label>
		<input id="new-todo-item-title" @keydown.enter="ajouterTodo"/>
		<button id="new-todo-item-add" @click.stop="ajouterTodo">Add</button>
	</div>
	<div id="edit-item" :hidden="!editMode">
		<h3>Edit todo item</h3>
		<label for="edit-todo-item-title">Title</label>
		<input id="edit-todo-item-title" :value="titres[currentEditIndex]"/>
		<button id="edit-todo-item-confirm" @click="confirmEdit">Confirm</button>
		<button id="edit-todo-item-cancel" @click="editMode = false">Cancel</button>
	</div>

</template>