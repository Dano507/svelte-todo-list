<script>
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();

  export let id = null;
  export let text = "[sample text]";
 
  export let state = false;  // expose checked state to parent
  
  // dispatch delete event
  const del = e => {
    dispatch('delete', {id: id});
  }

  const flipState = e => {
    state=!state;
  }
</script>


<div class="container" class:finished={state} on:click={flipState}>
  <div class="name-container">
    <input type="checkbox" class="checkbox" bind:checked={state}>
    <p>{text}</p>
  </div>

  <button on:click={del}>[del]</button>
</div>



<style>
.container {
  --padding: 12px;

  display: inline-flex;
  justify-content: space-between;
  box-sizing: border-box;

  padding: var(--padding);
  width: 100%;

  border-radius: 16px;
  border: solid #ccc 1px;
  background-color: #eee;

  filter: drop-shadow(0px 0px 4px #0003);
}
.finished {
  background-color: lightgreen;
}


.checkbox {
  height: 20px;
  width: 20px;
  background-color: blue;
}

.name-container {
  display: inline-flex;
  align-items: center;
  justify-content: center;
}
.name-container * { margin-right: var(--padding); }


button {
  border: none;
  background-color: transparent;
  padding: 0 4px;
}
button:hover { background-color: #fff; }
button:active { background-color: inherit; }
</style>
