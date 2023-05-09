<script>
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
