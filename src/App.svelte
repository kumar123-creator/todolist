<script>
  import { afterUpdate } from 'svelte';
  afterUpdate(() => {
    document.querySelector('.js-todo-input').focus();
  });
  let todoItems = [];
  let newTodo = '';
  function addTodo() {
    newTodo = newTodo.trim();
    if (!newTodo) return;
    const todo = {
      text: newTodo,
      checked: false,
      id: Date.now(),
    };
    todoItems = [...todoItems, todo];
    newTodo = '';
  }
  function toggleDone(id) {
    const index = todoItems.findIndex(item => item.id === Number(id));
    todoItems[index].checked = !todoItems[index].checked;
  }
  function deleteTodo(id) {
    todoItems = todoItems.filter(item => item.id !== Number(id));
  }
</script>

<main>
  <div class="container">
    <h1 class="app-title">todos</h1>
    <ul class="todo-list">
      {#each todoItems as todo (todo.id)}
        <li class="todo-item {todo.checked ? 'done' : ''}">
          <input id={todo.id} type="checkbox" />
          <label for={todo.id} class="tick" on:click={() => toggleDone(todo.id)}></label>
          <span>{todo.text}</span>
          <button class="delete-todo" on:click={() => deleteTodo(todo.id)}>
            <svg><use href="#delete-icon"></use></svg>
          </button>
        </li>
      {/each}
    </ul>
    <div class="empty-state">
      <svg class="checklist-icon"><use href="#checklist-icon"></use></svg>
      <h2 class="empty-state__title">Add your first todo</h2>
      <p class="empty-state__description">What do you want to get done today?</p>
    </div>
    <form on:submit|preventDefault={addTodo}>
      <input class="js-todo-input" type="text" aria-label="Enter a new todo item" placeholder="E.g. Build a web app" bind:value={newTodo}>
    </form>
  </div>
</main>
	let todos = [];
    let newTodoTitle = '';
  
	function addTodo() {
	  const newTodo = {
		id: todos.length + 1,
		title: newTodoTitle,
		completed: false
	  };
	  todos = [newTodo, ...todos];
	  newTodoTitle = '';
	}
  
	function toggleCompleted(todo) {
	  todo.completed = !todo.completed;
	  todos = [...todos];
	}
  
	function removeTodo(todo) {
	  todos = todos.filter(t => t.id !== todo.id);
	}
  </script>

  <main>
	<h1>Todo List</h1>
	<form on:submit|preventDefault={addTodo}>
	  <input type="text" bind:value={newTodoTitle} placeholder="Add a new todo" />
	  <button>Add</button>
	</form>
	{#if todos.length === 0}
	  <p>No todos</p>
	{:else}
	  <ul>
		{#each todos as todo (todo.id)}
		  <li
			class:completed={todo.completed}
			on:click={() => toggleCompleted(todo)}
		  >
			{todo.title}
			<button on:click={() => removeTodo(todo)}>X</button>
		  </li>
		{/each}
	  </ul>
	{/if}
  </main>

  <style>
	main {
	  display: flex;
	  flex-direction: column;
	  align-items: center;
	  margin-top: 2rem;
	}
  
	h1 {
	  font-size: 2rem;
	  margin-bottom: 1rem;
	}
  
	form {
	  display: flex;
	  justify-content: center;
	  margin-bottom: 1rem;
	}
  
	input[type="text"] {
	  font-size: 1rem;
	  padding: 0.5rem;
	  border-radius: 0.25rem;
	  border: none;
	  margin-right: 0.5rem;
	  width: 15rem;
	}
  
	button {
	  font-size: 1rem;
	  padding: 0.5rem;
	  border-radius: 0.25rem;
	  border: none;
	  background-color: #007bff;
	  color: #fff;
	  cursor: pointer;
	}
  
	ul {
	  list-style-type: none;
	  padding: 0;
	  margin: 0;
	}
  
	li {
	  display: flex;
	  align-items: center;
	  font-size: 1.2rem;
	  padding: 0.5rem;
	  border-radius: 0.25rem;
	  margin-bottom: 0.5rem;
	  background-color: #f8f9fa;
	  cursor: pointer;
	  transition: background-color 0.2s ease;
	}
  
	li.completed {
	  background-color: #28a745;
	  color: #fff;
	}
  
	li:hover {
	  background-color: #e9ecef;
	}
  
	button {
	  font-size: 1rem;
	  padding: 0.5rem;
	  border-radius: 0.25rem;
	  border: none;
	  background-color: #dc3545;
	  color: #fff;
	  cursor: pointer;
	  margin-left: auto;
	}
  
	button:hover {
	  background-color: #c82333;
	}
  </style>
