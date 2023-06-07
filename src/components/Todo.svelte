












<script>
  import { createClient } from '@supabase/supabase-js';
  import { onMount } from 'svelte';

  const supabaseUrl = 'https://qykjepghunztlqosthhi.supabase.co';
  const supabaseKey = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InF5a2plcGdodW56dGxxb3N0aGhpIiwicm9sZSI6ImFub24iLCJpYXQiOjE2ODYxMDE2MjYsImV4cCI6MjAwMTY3NzYyNn0.EosyWz-QnOzX3A7QutwKCg_zhtuV1-rjWgY6TA6TUbY';
  const supabase = createClient(supabaseUrl, supabaseKey);


  let totalTodos = 0;

  let newTask = '';
  let tasks = [];

  async function addTask() {
    const { data, error } = await supabase.from('todos').insert([{ titlem: newTask }]);

    if (error) {
      console.error('Error al agregar la tarea:', error.message);
    } else {
      console.log('Tarea agregada exitosamente:', data);
      tasks = [{ titlem: newTask }, ...tasks];
      newTask = '';
      totalTodos++;
    }
  }

  async function fetchTasks() {
    const { data, error } = await supabase.from('todos').select('titlem');

    if (error) {
      console.error('Error al obtener las tareas:', error.message);
    } else {
      tasks = data;
      totalTodos = data.length;
    }
  }

  onMount(fetchTasks);



  async function deleteTask(task) {
  const { error } = await supabase.from('todos').delete().match({ titlem: task.titlem });

  if (error) {
    console.error('Error al eliminar la tarea:', error.message);
  } else {
    console.log('Tarea eliminada exitosamente:', task);
    tasks = tasks.filter(t => t.titlem !== task.titlem);
    totalTodos--;
  }
}

</script>

<main>

  <form class="card__input-container" on:submit|preventDefault={addTask}>
      <input class="input" type="text" bind:value={newTask} placeholder="Add new todo..." />
    <button class="button" type="submit">Add</button>
  </form>


<div class="container__task">
  <ul>
    {#each tasks as task (task.titlem)}
      <li class="content__task">{task.titlem}
        <button class="button__delete" on:click={() => deleteTask(task)}>
        <img src="svg/delete.svg" alt="delete icon"/>
        </button>
      </li>
    {/each}
  </ul>

        

</div>
    <p class="card__result">Total Todos: {totalTodos} | Completed Todos: 0</p>
</main>


<style>
.card__input-container {
  display: flex;
  align-items: center;
  margin-bottom: 32px;
}
.input {
  flex-grow: 1;
  font-size: 16px;
  height: 43px;
  padding: 8px;
  
  border: 2px solid #9CA3AF;
  box-sizing: border-box;
  background-color: var(--input-color);
  border-radius: 6px 0 0 6px;
  outline: none
}

input::placeholder {
    color: #9CA3AF;
}
input {
  caret-color: white;
  color: white;
}


.button {
  background-color: #3B82F6;
  color: #fff;
  height: 43px;
  border: none;
  padding: 0px 24px;
  cursor: pointer;
  border-radius: 0 6px 6px 0;

  font-size: 16px;

}
.button:hover {
  background-color: #2563EB;
}
.container__task {
    padding-left: 32px;

    
}
.container__task ul {
    list-style: none;
}
.content__task {

    color: var(--text-color);
    font-family: 'Lato', sans-serif;
    font-weight: 400;
    display: flex;
    align-items: center;
    justify-content: space-between;
    background-color: var(--input-color);
    min-height: 24px;
    height: auto;
    padding: 16px;
    margin-bottom: 8px;
    border-radius: 6px;
}
li:last-child {
  margin-bottom: 28px;
}

.card__result {
  color: var(--text-color);
  font-family: 'Lato', sans-serif;
  font-weight: 400;
  margin-bottom: 20px;
}

.button__delete {
    border: none;
    background: none;
    display: flex;
    cursor: pointer;
}
</style>


























