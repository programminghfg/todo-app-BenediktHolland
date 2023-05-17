<script>
import { onMount } from 'svelte';
import { browser } from '$app/environment';
import ToDo from '../lib/components/ToDo.svelte';

    let todoText = "";
    let todos = [];

    let test;

    function saveTodoList(todoList) {
        localStorage.setItem('todoList', JSON.stringify(todoList));
    }

    function getTodoList() {
        const todoList = localStorage.getItem('todoList');
        return todoList ? JSON.parse(todoList) : [];
    }

    function addTodo() {
        const timestamp = new Date().toLocaleString(); // Get current timestamp
        todos.push({ text: todoText, done: false, timestamp: timestamp });
        todos = todos;
        todoText = "";
        saveTodoList(todos);
    }

    function remove(index) {
        // Delete entry
        todos.splice(index, 1);
        todos = todos;
    }
</script>

<h1>TODO APP</h1>

<!--textfeld-->
<input type="text" class="todo-input" bind:value={todoText} />

<!--button add-->
<button on:click={addTodo}>ADD</button>
<!--todo-->
{#each todos as todo, index}
    <ToDo todoData={todo} bind:testProp={test} {index} on:removeEvent={remove} />
{/each}
<!-- text -->
<!-- checkboxen -->
<style>
    * {
        font-family: Arial, Helvetica, sans-serif;
    }

</style>
