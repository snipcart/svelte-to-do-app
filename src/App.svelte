<script>
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

    console.log(todoList);
  }
</script>

<main class="container">
	<main class="container">
		<div>
		  <form on:submit|preventDefault={addTodo}>
			<input
			  bind:value={newItem}
			  type="task"
			  class="todos__input"
			  placeholder="Enter Todo"
			/>
			<button class="todos__button">+</button>
		  </form>
		  <h2 class="todos__listHeader">My to-do list</h2>
		</div>
		{#each todoList as item, index}
		<div class="todo">
		  <span class="todo__text">{item.task}</span>
		</div>
	  {/each}
	  </main>

</main>

<style>
 .todos__listHeader {
    text-align: center;
    padding: 20px;
    border-radius: 20px;
    box-shadow: 0 0 15px rgb(0 0 0 / 20%);
    background-color: hsla(0, 0%, 100%, 0.2);
    -webkit-backdrop-filter: blur(25px);
    backdrop-filter: blur(25px);
    margin: 15px 0px 25px 0px;
    font-size: 1.2rem;
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


  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
    min-height: 90vh;
    background: #222e50
      url(https://images.unsplash.com/photo-1631398741662-3e0a047c6c5f?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1470&q=80)
      no-repeat;
    background-size: cover;
    padding-top: 10vh;
  }

  .todos__input {
    background-color: inherit;
    border: none;
    box-shadow: none;
    text-decoration: none;
    font-size: 1.2rem;
    border-bottom: 1px solid black;
    margin-top: 15px;
    outline: none;
    width: 500px;
  }
  .todos__button {
    background-color: inherit;
    border: none;
    box-shadow: none;
    font-size: 1.2rem;
    cursor: pointer;

  }
  
</style>
