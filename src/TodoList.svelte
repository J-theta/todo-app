<script>
  import store from './store.js';
  import { fly } from 'svelte/transition'
  export let todos;

  const deleteTodo = (index) => {
    todos = store.get('/todos', { where: (t, i) => i !== index });
    store.set('/todos', todos);
  }

  const toggleTodo = (index) => {
    todos = [...todos].map((t, i) => i === index ? { ...t, completed: !t.completed } : t);
    store.set('/todos', todos);
  }
  export let theme;
</script>

<div class="todo-list" { theme }>
  <ul>
    {#each todos as { text, completed }, i}
      <li class:completed={completed} transition:fly={{ x: -100 }}>
        <div class="text">
          { text }
        </div>
        <div class="btn" on:click={() => toggleTodo(i)}>
          <i 
            class="mdi"
            class:mdi-checkbox-blank-circle-outline={!completed}
            class:mdi-check-circle-outline={completed}></i>
        </div>
        <div class="btn-delete" on:click={() => deleteTodo(i) }>
          <i class="mdi mdi-delete-forever"></i>
        </div>
      </li>
    {/each}
  </ul>
</div>

<style>
  .todo-list {
    width: 90%;
    min-width: 400px;
    max-width: 800px;
  }

  .todo-list ul {
    margin: 0;
    padding: 0;
    list-style-type: none;
  }

  li {
    display: grid;
    padding: 10px 5px 10px 10px;
    grid-template-columns: auto 40px 40px;
    align-items: center;
    box-shadow: 0 2px 6px #32323234;
    border-radius: 10px;
    margin-bottom: 10px;
    transition: all 200ms ease;
  }

  li .btn, li .btn-delete {
    display: grid;
    justify-content: center;
    cursor: pointer;
    font-size: 1.2em;
    transition: font-size 200ms ease;
  }

  .btn:hover, .btn-delete:hover {
    font-size: 1.5em;
  }

  li.completed {
    text-decoration: line-through;
    background: var(--s);
    color: whitesmoke
  }

  .todo-list[theme=dark] li {
    background: var(--p);
    color: var(--s);
  }
  .todo-list[theme=dark] li.completed {
    background: var(--s);
    color: var(--p);
  }
</style>