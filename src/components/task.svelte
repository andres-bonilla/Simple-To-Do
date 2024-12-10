<script>
  export let checkTask = () => {}
  export let removeTask = () => {}
  export let item = {
          id: "",
          text: "",
          state: false
        }
</script>

<li class= { item.state ? "task-on taskBox" : "task-off taskBox" } >
  <p>
    { item.text }
  </p>
  <div class="buttons">
    <button class="inlineButton" on:click={ () => { checkTask( item.id ) } }>
      {#if item.state}
        <img src="src/essets/on.svg" alt="onIcon"/>
      {:else}
        <img src="src/essets/off.svg" alt="offIcon"/>
      {/if}
    </button>
    <button class="inlineButton" on:click = { () => { removeTask( item.id ) } }>
      <img src="src/essets/trash.svg" alt="trashIcon"/>
    </button>
  </div>
</li>

<style  lang="scss">
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
    background-color: hsl(221, 37%, 80%)/*#fbf5f3*/;
    margin: 7px auto;
    border: 2px solid #34373c/*rgb(255, 62, 0)*/;
    p {
      color: hsl(220, 7%, 22%)/*rgb(255, 62, 0)*/;
    }
  }
  .task-on {
    background-color: hsl(221, 37%, 45%)/*#fbf5f3*/;
    margin: 8px auto;
    border: 2px solid /*rgb(255, 62, 0)rgba(255, 191, 169, 0.3)*/#34373c;
    p {
      color: #34373c
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