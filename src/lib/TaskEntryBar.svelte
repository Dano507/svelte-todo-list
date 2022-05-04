<script>
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();

  export let value = "";

  const entry = text => {
    dispatch('entry', {text: text})
  }
  const taskInputKeypressHandler = e => { 
    if (e.key === "Enter") { 
      entry(e.target.value);
      e.target.value = "";
    }
  }
</script>



<input type="text" class="task-input" placeholder="New Task . . ."
  bind:value
  on:keypress={taskInputKeypressHandler}
>

<style>
  .task-input {
    height: 30px;
    min-width: 14rem;
    width: 28vw;

    padding: 10px;

    border: solid #bbb 1px;
    background-color: #eee;

    filter: drop-shadow(0px 0px 4px #0003);
  }
</style>