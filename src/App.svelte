<svelte:head>
  <link rel="stylesheet" href="//cdn.materialdesignicons.com/5.0.45/css/materialdesignicons.min.css">
</svelte:head>

<script>
  import TodoList from './TodoList.svelte'
  import NewTodo from './NewTodo.svelte'
  import store from './store.js';
  let todos = store.get('/todos');
  let theme = store.get('/theme');

  const onnewtodo = () => {
    todos = store.get('/todos');
  }

  const toggleTheme = () => {
    const dark = theme === 'dark';
    if (dark) store.set('/theme', 'light')
    else store.set('/theme', 'dark')
    theme = store.get('/theme');
  }
  
</script>

<main>
	<h1>Todo App</h1>
  <div class="theme" on:click={toggleTheme}>
    <span>Dark theme </span>
    <i class="mdi" 
    class:mdi-checkbox-blank-circle-outline={theme === 'light'}
    class:mdi-check-circle-outline={theme === 'dark'}></i>
  </div>
  <NewTodo { theme } on:new-todo={onnewtodo} />
  <TodoList { theme } todos={todos} />
</main>

<style>
  main {
    display: grid;
    grid-template-rows: auto;
    grid-auto-columns: auto;
    justify-content: center;
    align-items: center;
    align-content: center;
    row-gap: 10px;
    color: var(--p);
  }

  h1 {
    text-align: center;
    color: #454460;
  }

  .theme {
    font-size: 1.2em;
    padding: 10px;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    cursor: pointer;
  }

</style>
