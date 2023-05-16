<script>
    let todoText = "";
    let todos = [];

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
    <div class="todo-entry" class:done={todo.done}>
        <input type="checkbox" bind:value={todo.done} />
        <div class="todo-text">{todo.text}</div>
        <div class="timestamp">{todo.timestamp}</div> <!-- Display timestamp -->
        <button class="delete" on:click={() => { remove(index); }}>X</button>
    </div>
{/each}
<!-- text -->
<!-- checkboxen -->
<style>
    * {
        font-family: Arial, Helvetica, sans-serif;
    }

    .delete {
        background-color: white;
        border: none;
    }

    .delete:hover {
        background-color: green;
        border-radius: 5px;
    }

    .done {
        color: grey;
    }

    .todo-entry {
        display: flex;
        align-items: center;
    }
    
    .timestamp {
        font-size: 12px;
        color: gray;
        margin-top: 4px;
        margin-left: 5px;
    }
    
    .done .todo-text {
        margin-left: 100px; 
        color: green;
    }
</style>
