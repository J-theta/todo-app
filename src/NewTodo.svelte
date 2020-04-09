<script>
  import store from './store.js';
  import { createEventDispatcher } from 'svelte'
  let text = '';
  let dispatch = createEventDispatcher();
  const addTodo = () => {
    if (text.trim() !== '') {
      store.add('/todos', {
        text: text.length > 30 ? text.slice(0, 30) + '...' : text,
        completed: false
      })
      dispatch('new-todo', {})
    }
  }
  export let theme;
</script>

<div class="new-todo" { theme }>
  <input type="text" placeholder="New todo" name="new-todo" bind:value={text}/>
  <div class="add" on:click={addTodo}>
    <i class="mdi mdi-plus-circle"></i>
  </div>
</div>

<style>
  .new-todo {
    display: grid;
    grid-template-columns: auto 50px;
    align-items: center;
    border-radius: 50px;
    border: 2px solid var(--p);
    color: var(--p);

  }

  .new-todo input {
    border-radius: 5px;
    color: inherit;
    padding: 10px 15px 10px 15px;
    margin: 0;
    border: none;
    background: transparent;
  }

  .new-todo .add {
    display: flex;
    justify-content: center;
    align-content: center;
    font-size: 1.7em;
    cursor: pointer;
  }

  .new-todo .add i {
    height: max-content;
    margin: auto;
  }

  .new-todo[theme=dark] {
    background: var(--p);
    color: var(--s);
  }
</style>