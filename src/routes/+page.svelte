<script>
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
  
  $: browser 
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

  {#each todoList as item}
    <div class= {item.state ? "task-on taskBox" : "task-off taskBox"}>
      <p>
        {item.text}
      </p>
      <div class="buttons">
        <button class="inlineButton" on:click={() => { checkTask( item.id ) }}>
          { #if item.state }
          <img src="src/essets/on.svg" alt="onIcon"/>
          {:else}
          <img src="src/essets/off.svg" alt="offIcon"/>
          {/if}
        </button>
        <button class="inlineButton" on:click={()=>{ removeTask( item.id )}}>
          <img src="src/essets/trash.svg" alt="trashIcon"/>
        </button>
      </div>
    </div>
  {/each}
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
    padding: 10px 12px;
    border-radius:12px;
    margin-bottom: 24px;
    font-size: 20px;
  }
  p {
    width: 70%;
    margin: 12px 0px 12px 12px;
    font-size: 22px;
    font-weight: 400;
    text-align: left;
  }
  .taskBox {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 65%;
    min-width: 340px;
    border-radius:12px;
  }
  .task-off {
    margin: 7px auto;
    border: 2px solid rgb(255, 62, 0);
    background: rgb(255, 238, 228);
    p {
      color: rgb(255, 62, 0);
    }
  }

  .task-on {
    margin: 8px auto;
    border: 1px solid rgb(255, 62, 0);
    background: rgb(255, 248, 244);
    p {
      color: rgb(255, 191, 169)
    }
  }
  .inlineButton {
    display:inline-block;
    all: unset;
    cursor: pointer;
    img {
      margin-right: 15px;
    }
  }
  .inlineButton:active {
    background:#fff6f1;
  }
</style>