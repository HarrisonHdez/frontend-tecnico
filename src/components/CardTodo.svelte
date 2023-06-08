<script>

  import Quote from './Quote.svelte';
  import Todo from './Todo.svelte';


  let title = 'TaskMaster';

  
  

</script>

<div class="card">
    <div class="card__content-container">
      <div class="card__content">
        <h1 class="card__title">{title}</h1>
        
        
        <Todo on:todoAdded={(event) => console.log('Todo added:', event.detail)} />
        
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










</style>


