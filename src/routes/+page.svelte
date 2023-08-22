<script>
  let todo = {
    id: "",
    text: "",
    state: false
  }, todoList = []
  const addTodo = ()=>{
    if (todo.text.trim()){
      todo.id = Date.now()
      todoList = [ ...todoList, todo]
      todo = {
        id: "",
        text: "",
        state: false
      }
    }
    todo.text = ""
  }
  $: console.log(todo.text)
</script>

<main> 
  <h1>Simple TO-DO</h1>
  
  <form on:submit|preventDefault={ addTodo }>
    <input 
    type="text" 
    placeholder="Add task..." 
    bind:value= {todo.text}
    />
  </form>

  {#each todoList as item}
    <div>
      <p>
        {item.text}
      </p>
    </div>
  {/each}
</main>