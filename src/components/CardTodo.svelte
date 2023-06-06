<script>
  let title = 'TaskMaster';
  let description = '';
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
        <p class="description">{description}</p>
        
        <div class="input-container">
          <input type="text" bind:value={inputValue} class="input" placeholder="Ingrese un valor" />
          <button aria-label="Agregar Tarea" on:click={handleAdd} class="button">Add</button>
        </div>

        <p class="card__result">Total Todos: 0 | Completed Todos: 0</p>
        <p class="card__paragraph">"I think it is possible for ordinary people to choose to be extraordinary." - Elon Musk</p>
      </div>
    </div>
</div>

<style>
.card {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
}
 
.card__content-container {
    max-width: 512px;
    width: 100%;
    min-height: 283px;
    height: auto;
    background-color: var(--primary-color);
    border-radius: 8px;

    box-shadow: 0px 0px 80px 10px rgba(0, 0, 0, 0.2); 

}
.card__content {
    height: 100%;
    padding: 24px;
}

.card__title {
    font-size: 24px;
    margin-bottom: 10px;
    color: var(--text-color);

    font-family: 'Lato', sans-serif;
    font-weight: 900;
}

  .description {
    font-size: 16px;
    margin-bottom: 20px;
  }

  .input-container {
    display: flex;
    align-items: center;
  }

  .input {
    flex-grow: 1;
    height: 30px;
    margin-right: 10px;
    padding: 4px 8px;
    border: 1px solid #ccc;
    box-sizing: border-box;
  }

  .button {
    background-color: #007bff;
    color: #fff;
    border: none;
    padding: 8px 16px;
    cursor: pointer;
  }




.card__result {
    color: #fff;
}
.card__paragraph {
    color: #fff;
}
</style>


