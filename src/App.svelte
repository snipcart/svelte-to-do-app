<script>
  import Icon from "./Icon.svelte";

  let newItem = "";
  let todoList = [
    {
      task: "Do my laundry",
      completed: false,
    },
    {
      task: "Sniff a flower",
      completed: true,
    },
  ];

  function add() {
    if (newItem !== "") {
      todoList = [
        ...todoList,
        {
          task: newItem,
          completed: false,
        },
      ];
      newItem = "";
    }
  }
  function complete(item) {
    item.completed = !item.completed;
  }
  function remove(index) {
    todoList.splice(index, 1);
    todoList = todoList;
  }
</script>

<main>
  <!-- Header -->
  <h1>My to-do list</h1>

  <!-- Form -->
  <form on:submit|preventDefault={add}>
    <input bind:value={newItem} placeholder="Enter to-do" />
    <button class="add-todo" on:click={add}><span>+</span></button>
  </form>

  <!-- To-dos -->
  <div class="todos">
    {#each todoList as item, index}
      <div class="todo" class:completed={item.completed}>
        <span class="todo__text">{item.task}</span>
        <div class="todo__buttons">
          <button class="complete" on:click={() => complete(item)}>
            <Icon name="check-mark" />
          </button>
          <button class="delete" on:click={() => remove(index)}>
            <Icon name="delete" />
          </button>
        </div>
      </div>
    {/each}
  </div>
</main>

<style>
  main {
    display: flex;
    flex-direction: column;
    align-items: center;
    min-height: 100%;
    padding: 5vmin;
    box-sizing: border-box;
    background: antiquewhite;
  }
  h1 {
    text-align: center;
    font-size: 1.5rem;
    margin: 2em 0;
  }

  form {
    width: 100%;
    max-width: 500px;
    display: flex;
    align-items: center;
    margin-bottom: 1rem;
  }

  input {
    flex-grow: 1;
    width: 0;
    border: none;
    border-bottom: 1px solid black;
    background: transparent;
    box-shadow: none;
    font-size: 1.2rem;
    margin: 0;
    outline: none;
  }

  button.add-todo {
    width: 2rem;
    height: 2rem;
    margin: 0;
    background: transparent;
    border: 1px solid black;
    border-radius: 100%;
    flex-shrink: 0;
    margin-left: 1rem;
  }

  button.add-todo span {
    display: flex;
    align-items: center;
    justify-content: center;
    line-height: 0;
  }

  .todos {
    width: 100%;
    max-width: 500px;
  }
  .todo {
    display: flex;
    padding: 20px;
    border-radius: 20px;
    box-shadow: 0 0 15px rgb(0 0 0 / 20%);
    background-color: hsla(0, 0%, 100%, 0.2);
    margin-top: 1rem;
    font-size: 1.2rem;
    justify-content: space-between;
    align-items: center;
  }

  .todo__buttons {
    display: flex;
    align-items: center;
    margin-left: 1rem;
  }

  .todo button {
    width: 32px;
    height: 32px;
    padding: 4px;
    margin: 0;
    flex-shrink: 0;
  }

  .todo.completed {
    color: slategray;
  }
  .todo.completed .todo__text {
    text-decoration: line-through;
  }
  .todo.completed button {
    color: silver;
  }

  button.delete,
  button.delete:hover {
    color: brown;
    transition: color 100ms ease-out;
  }
  button.complete,
  button.complete:hover {
    color: cadetblue;
    transition: color 100ms ease-out;
  }
</style>
