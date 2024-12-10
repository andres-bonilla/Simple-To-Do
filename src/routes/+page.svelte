<script>
  import Task from '../components/task.svelte';
  import { browser } from '$app/environment';

  let todo = {
    id: "",
    text: "",
    state: false
  }, todoList = []
  
  const addTask = () => {
    if ( todo.text.trim() ){
      todo.id = Date.now()
      todoList = [ todo, ...todoList ]
      todo = {
        id: "",
        text: "",
        state: false
      }
    }
    todo.text = ""
  }

  const removeTask = id => {
    todoList = todoList.filter( task => 
		  task.id !== id
    )
  }

  const checkTask = id => {
    todoList = todoList.map( task => 
      task.id === id 
      ? { ...task, state: !task.state } 
      : task 
    )
  }

  if (browser && localStorage.getItem("todos") )
    todoList = JSON.parse( localStorage.getItem( "todos" ) ) || todoList
  
  $:browser 
    ? localStorage.setItem("todos", JSON.stringify( todoList ) ) 
    : console.log("Browser ERROR")
</script>

<main> 
  <h1>Simple TO-DO</h1>
  
  <form on:submit|preventDefault={ addTask }>
    <input 
    type="text" 
    placeholder="Add task..." 
    bind:value= {todo.text}
    />
  </form>

  <ul>
    {#each todoList as item}
      <Task { item } { checkTask } { removeTask }/>
    {/each}
  </ul>
</main>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css2?family=Maven+Pro&display=swap');
  main {
    min-width: 340px;
    font-family: 'Maven Pro', sans-serif;
    text-align: center;
  }
  h1 {
    margin: 32px auto;
    font-size: 44px;
    font-weight: 100;
    color: rgb(255, 62, 0);
  }
  input {
    width: 50%;
    min-width: 270px;
    padding: 8px 12px;
    border-radius:12px;
    margin-bottom: 24px;
    font-size: 22px;

    border: 2px solid rgb(255, 62, 0);
  }
</style>