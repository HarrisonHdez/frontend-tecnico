












<script>
  import { createClient } from '@supabase/supabase-js';
  import { onMount } from 'svelte';

  const supabaseUrl = 'https://qykjepghunztlqosthhi.supabase.co';
  const supabaseKey = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InF5a2plcGdodW56dGxxb3N0aGhpIiwicm9sZSI6ImFub24iLCJpYXQiOjE2ODYxMDE2MjYsImV4cCI6MjAwMTY3NzYyNn0.EosyWz-QnOzX3A7QutwKCg_zhtuV1-rjWgY6TA6TUbY';
  const supabase = createClient(supabaseUrl, supabaseKey);

  let completedTodos = 0;
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
  const { data, error } = await supabase.from('todos').select('titlem, status');

  if (error) {
    console.error('Error al obtener las tareas:', error.message);
  } else {
    tasks = data;
    totalTodos = data.length;

    // Contar el número de tareas completadas
    completedTodos = tasks.filter(task => task.status).length;
  }
}




  onMount(fetchTasks);

  function updateCompletedTodos() {
  completedTodos = tasks.filter(task => task.status).length;
}




  async function deleteTask(task) {
  const { error } = await supabase.from('todos').delete().match({ titlem: task.titlem });

  if (error) {
    console.error('Error al eliminar la tarea:', error.message);
  } else {
    console.log('Tarea eliminada exitosamente:', task);
    tasks = tasks.filter(t => t.titlem !== task.titlem);
    totalTodos--;
    updateCompletedTodos();
  }
}

async function completeTask(task) {
  const { data, error } = await supabase
    .from('todos')
    .update({ status: true })
    .match({ titlem: task.titlem });

  if (error) {
    console.error('Error al marcar la tarea como completada:', error.message);
  } else {
    console.log('Tarea marcada como completada exitosamente:', task);
    tasks = tasks.map(t => {
      if (t.titlem === task.titlem) {
        return { ...t, status: true };
      }
      return t;
    });
    updateCompletedTodos();
  }
}




</script>

<main>

  <form class="card__input-container" on:submit|preventDefault={addTask}>
      <input class="input" type="text" bind:value={newTask} placeholder="Add new todo..." required/>
    <button class="button" type="submit">Add</button>
  </form>



<div class="container__task">
  <ul>
    {#each tasks as task }
      <li class="content__task">
        <span class={task.status ? 'completed-task' : ''}>{task.titlem}</span>
        <div class="button__container">
        
        
            {#if !task.status}
            <button class="button__complete" on:click={() => completeTask(task)}>
                <img src="svg/check.svg" alt="complete" />
            </button>
            {/if}
            <button class="button__delete" on:click={() => deleteTask(task)}>
                <img src="svg/delete.svg" alt="Delete" />
            </button>
        </div>

      </li>
    {/each}
  </ul>
</div>





    <p class="card__result">Total Todos: {totalTodos} | Completed Todos: {completedTodos}</p>

</main>


<style>
.completed-task {
  text-decoration: line-through;
}

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
.button__container {
    display: flex;
    align-items: center;
}
.button__complete {
     border: none;
    background: none;
    display: flex;
    cursor: pointer;
}
.button__delete {
    border: none;
    background: none;
    display: flex;
    cursor: pointer;
}
</style>


























