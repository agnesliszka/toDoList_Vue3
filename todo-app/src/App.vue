<template>
<div>
  <h1>Vue 3 Todo App</h1>
  <form @submit.prevent=addNewTodo>
    <label>New Todo</label>
    <input v-model="newTodo" name="newTodo">
    <button>Add New Todo</button>
  </form>
  <button @click="removeAllTodos">Remove all</button>
  <button @click="markAllDone">Mark all done</button>
  <ul>
  <li v-for="(todo, index) in todos" :key="index" class="todo">  
    <h3 :class="{done : todo.done}" @click="toggleDone(todo)">{{todo.content}}</h3>
    <button @click="removeTodo(index)">Remove todo</button>
  </li>
  </ul>

  </div>
</template>

<script>
import { ref } from 'vue';

export default {


setup() {
  const newTodo = ref('');
  const todos = ref([]);

   function addNewTodo() {
     todos.value.push({
       done: false,
       content: newTodo.value
     });
     newTodo.value=''
   }

   function toggleDone(todo){
     todo.done = !todo.done; 
   }

    function removeTodo(index) {
      todos.value.splice(index, 1);
    }

  function markAllDone() {
      todos.value.forEach((todo) => {todo.done = true});
    }

    function removeAllTodos() {
      todos.value = []
    }

   return {
    newTodo,
    todos,
    addNewTodo,
    toggleDone,
    removeTodo,
    markAllDone,
    removeAllTodos
   };
 }

}
</script>

<style>
body {
  font-family: sans-serif;
  padding-top: 1em;
  padding-bottom: 1em;
  font-size: 2em;
  width: 80%;
  margin: 0 auto;
}
input, textarea, button, p, div, section, article, select {
  display: 'block';
  width: 100%;
  font-family: sans-serif;
  font-size: 1em;
  margin: 0.5em;
}
.todo {
  cursor: pointer;
}

.done {
  text-decoration: line-through;
}
</style>
