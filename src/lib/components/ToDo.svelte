<script>
import { createEventDispatcher } from 'svelte';

export let todoData = undefinded;
export let index = undefined;
export const testProp = 'das is ein test'

const dispatch = createEventDispatcher();

function triggerDelete() {
    dispatch ('removeEvent',index);
}


</script>

<div  class="todo-entry" class:done={todoData.done}>

    <input type="checkbox" bind:value={todoData.done} />
        <div class="todo-text">{todoData.text}</div>
        <div class="timestamp">{todoData.timestamp}</div> <!-- Display timestamp -->
        <button class="delete" on:click={() => { triggerDelete(index); }}>X</button>

</div>

<slot />

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
