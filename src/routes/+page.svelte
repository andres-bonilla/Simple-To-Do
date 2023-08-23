<script>
   let todo = {
    id: "",
    text: "",
    state: false
  }, todoList = []
  
  const addTask = () => {
    if ( todo.text.trim() ){
      todo.id = Date.now()
      todoList = [ ...todoList, todo ]
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
    <div class={item.state ? "task-on" : "task-off" }>
      <p>
        {item.text}
      </p>
      <button class="inline" on:click={() => { checkTask( item.id ) }}>
        { #if item.state }
          <img src="src/essets/on.svg" alt="onIcon"/>
        {:else}
          <img src="src/essets/off.svg" alt="offIcon"/>
        {/if}
      </button>
      <button class="inline" on:click={()=>{ removeTask( item.id )}}>
        <img src="src/essets/trash.svg" alt="trashIcon"/>
      </button>
    </div>
  {/each}
</main>

<style lang="scss">
  h1 {
    color: rgb(255, 62, 0);
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
    margin: 20px auto;
  }
  p {
    font-size: 22px;
    text-align: left;
    font-weight: 400;
    width: 360px;
  }
  .task-off {
    margin: 7px auto;
    background: rgb(255, 238, 228);
    border: 2px solid rgb(255, 62, 0);
    p {
      color: rgb(255, 62, 0);
    }
  }

  .task-on {
    margin: 8px auto;
    background: rgb(255, 248, 244);
    border: 1px solid rgb(255, 62, 0);
    p {
      color: rgb(255, 191, 169)
    }
  }

  .inline {
    display:inline-block;
    margin: 10px;
  }
</style>