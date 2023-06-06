<script>
  import Quote from './Quote.svelte';

  let title = 'TaskMaster';
  let inputValue = '';

  function handleAdd() {
    // Aquí puedes agregar la lógica para manejar el evento de "Add"
    console.log('Se ha hecho clic en el botón "Add"');
    console.log('Valor del input:', inputValue);
    // Puedes realizar otras operaciones, como enviar el valor a una API, etc.
  }
</script>

<div class="card">
    <div class="card__content-container">
      <div class="card__content">
        <h1 class="card__title">{title}</h1>
        
        <div class="card__input-container">
          <input type="text" bind:value={inputValue} class="input" placeholder="Add a new todo..." />
          <button aria-label="Agregar Tarea" on:click={handleAdd} class="button">Add</button>
        </div>

        <p class="card__result">Total Todos: 0 | Completed Todos: 0</p>
        
        <Quote />

        
      </div>
    </div>
</div>

<style>
.card {
  min-height: 100vh;
  padding: 50px 0;
  height: auto;
  display: flex;
  justify-content: center;
  align-items: center;
}
 
.card__content-container {
  max-width: 512px;
  width: 100%;
  height: auto;
  background-color: var(--primary-color);
  border-radius: 8px;

  box-shadow: 0px 0px 80px 10px rgba(0, 0, 0, 0.2); 

}
.card__content {
  padding: 24px;

  min-height: 283px;
  height: auto;
}

.card__title {
  font-size: 24px;
  margin-bottom: 24px;
  color: var(--text-color);

  font-family: 'Lato', sans-serif;
  font-weight: 900;
}


.card__input-container {
  display: flex;
  align-items: center;
  margin-bottom: 24px;
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




.card__result {
  color: var(--text-color);
  font-family: 'Lato', sans-serif;
  font-weight: 400;
  margin-bottom: 20px;
}

</style>


