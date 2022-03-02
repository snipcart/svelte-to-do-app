<script>
  import Icon from "./Icon.svelte";

  let newItem = "";
  let todoList = [];

  function addTodo() {
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
  function removeFromList(index) {
    todoList.splice(index, 1);
    todoList = todoList;
  }
</script>

<main>
  <!-- Header -->
  <h1>My to-do list</h1>

  <!-- Form -->
  <form on:submit|preventDefault={addTodo}>
    <input bind:value={newItem} placeholder="Enter to-do" />
    <button class="add-todo" on:click={addTodo}><span>+</span></button>
  </form>

  <!-- To-dos -->
  {#each todoList as item, index}
    <div class="todo" class:completed={item.completed}>
      <span class="todo__text">{item.task}</span>

      <div class="icons">
        <button
          class="icon__button"
          on:click={() => (item.completed = !item.completed)}
        >
          <Icon name="check-mark" />
        </button>
        <button class="icon__button" on:click={() => removeFromList(index)}>
          <Icon name="delete" />
        </button>
      </div>
    </div>
  {/each}
</main>

<style>
  main {
    display: flex;
    flex-direction: column;
    align-items: center;
    min-height: 100%;
    padding: 5vmin;
    box-sizing: border-box;
    background: #ffeda4;
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
  }

  button.add-todo span {
    display: flex;
    align-items: center;
    justify-content: center;
    line-height: 0;
  }
  .todo {
    display: flex;
    padding: 20px;
    border-radius: 20px;
    box-shadow: 0 0 15px rgb(0 0 0 / 20%);
    background-color: hsla(0, 0%, 100%, 0.2);
    -webkit-backdrop-filter: blur(25px);
    backdrop-filter: blur(25px);
    width: inherit;
    margin-top: 15px;
    font-size: 1.2rem;
    justify-content: space-between;
    align-items: center;
  }
  .todos__button {
    background-color: inherit;
    border: none;
    box-shadow: none;
    font-size: 1.2rem;
    cursor: pointer;
  }
  .icon__button {
    background-color: transparent;
    border: none;
    box-shadow: none;
    font-size: 1.2rem;
    cursor: pointer;
    color: rgba(0, 0, 0, 0.54);
  }
  .icon {
    background: rgba(0, 0, 0, 0.54);
  }

  .icon__button {
    width: 24px;
    height: 24px;
    padding: 0;
    margin: 0;
  }

  .todo.completed {
    text-decoration: line-through;
  }
</style>
