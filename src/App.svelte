<script lang=ts>
import { crossfade } from 'svelte/transition';
import ListItem from './lib/ListItem.svelte';
import TaskEntryBar from './lib/TaskEntryBar.svelte';

const [send, receive] = crossfade({
  duration: d => Math.sqrt(d * 200),
  fallback: (node) => {
    return { css: t=> `opacity: ${t};` }
  }
});

// sample tasks
let uid = 0;
let tasks = [
  {id: uid++, name: "example", done: true},
  {id: uid++, name: "tasks", done: false},
  {id: uid++, name: "Organise Fridge", done: false},
];


// Tasks methods
// Handle removing array elements
const handleRemove = e => {
  const id = e.detail.id

  tasks = tasks.filter((el, index) => {
    if (id !== el.id) {
      return el;
    }
  });
}

const newTask = name => {
  tasks = [...tasks, {id: uid++, name: name, done: false}];
}
const entryHandler = e => {
  newTask(e.detail.text)
}
</script>


<div class="app">
  <h1>TODO List</h1>

  <div class="task-container">
    <div class="unfinished">
      <h2>Unfinished</h2>
      {#each tasks.filter(t=>!t.done) as task, id (task.id)}
        <div out:send={{key: task.id}} in:receive={{key: task.id}}>
          <ListItem on:delete={handleRemove} bind:state={task.done}
            id={task.id} text={task.name} />
        </div>
      {/each}
    </div>

    <div class="finished">
      <h2>Finished</h2>
      {#each tasks.filter(t=>t.done) as task, id (task.id)}
        <div out:send={{key: task.id}} in:receive={{key: task.id}}>
          <ListItem on:delete={handleRemove} bind:state={task.done}
            id={task.id} text={task.name} />
        </div>
      {/each}
    </div>
  </div>

  <div id="taskEntry" class="task-entry">
    <TaskEntryBar on:entry={entryHandler} />
  </div>
</div>




<style>
  .task-container .unfinished,
  .task-container .finished {
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    gap: 12px;

    width: 100%;
    max-width: 20rem;

    transition: 0.4s;
  }
  .task-container {
    display: flex;
    flex-direction: row;
    justify-content: center;
    gap: 12px;

    width: 80%;
  }
  

  .app {
    display: flex;
    align-items: center;
    flex-direction: column;

    min-height: 100vh;
  }

  h1 {
    margin: 1.4rem 0;

    color: #ff6600;
    font-size: 3.2rem;
    font-weight: lighter;
  }


  .task-entry {
    position: absolute;
    bottom: 24px;

    display: block;

  }
</style>
