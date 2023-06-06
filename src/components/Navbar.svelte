<script>
  let icons = [
    { name: 'Icono1', icon: '/image/perfil.png' },
    { name: 'Icono2', icon: '/svg/arrow.svg' },

  ];
</script>

<nav class="nav">
    <div class="nav__content container">

        <div class="nav__logo-container">
            <span class="nav__logo">TaskMaster</span>
        </div>

        

        <div class="nav__icons">
            {#each icons as icon}
                <img src={icon.icon} alt={icon.name} class="nav__icon" class:clicked={icon.clicked} on:click={() => icon.clicked = !icon.clicked} />
            {/each}
        </div>
    </div>
  
</nav>

<style>
 nav {
    width: 100%;
    background-color: var(--primary-color);
    height: 48px;
  }
.nav__content {
    display: flex;  
    justify-content: space-between;
    align-items: center;
    color: white;
    height: 100%;
}
.nav__logo-container {

}

.nav__logo {
    
    font-size: 18px;
    font-family: 'Lato', sans-serif;
    font-weight: 700;
}
.nav__icons {
    display: flex;
    gap: 15px;
}
.nav__icons img {
    background: #374151;
    border-radius: 50%; 
    padding: 4px;
    cursor: pointer;

    width: 24px;
    height: 24px;
}

.nav__icon {
    border: none;
}

.nav__icon.clicked {
    border: 2px solid white;
}

</style>
