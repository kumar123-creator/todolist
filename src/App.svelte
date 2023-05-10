<script>
  let todos = [];
  let newTodo = '';

  function addTodo() {
    todos = [...todos, { text: newTodo, done: false }];
    newTodo = '';
  }

  function removeTodo(index) {
    todos = todos.filter((_, i) => i !== index);
  }
</script>

<div>
  <h1>Todo List</h1>
  <input bind:value={newTodo} placeholder="Add a new todo" />
  <button on:click={addTodo}>Add</button>

  <ul>
    {#each todos as todo, i}
      <li>
        <input type="checkbox" bind:checked={todo.done} />
        {todo.text}
        <button on:click={() => removeTodo(i)}>X</button>
      </li>
    {/each}
  </ul>
</div>
