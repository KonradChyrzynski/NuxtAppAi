<script setup>
const mobileMenu = ref(false)

const showMenu = () => {
  mobileMenu.value = !mobileMenu.value
}

</script>

<template>
    <nav class="navbar" role="navigation" aria-label="main navigation">
  <div class="navbar-brand">
    <a class="navbar-item">
      <img src="http://localhost:3000/logo.png" height="28">
    </a>

    <a role="button" 
    class="navbar-burger" 
    aria-label="menu" 
    aria-expanded="false" 
    data-target="navbarBasicExample"
    @click="showMenu"
    >
      <span aria-hidden="true"></span>
      <span aria-hidden="true"></span>
      <span aria-hidden="true"></span>
    </a>
  </div>

  <div id="navbarBasicExample" :class="{'navbar-menu': !mobileMenu}">
    <div class="navbar-start">
      <NuxtLink to="/" class="navbar-item">
        Strona domowa
      </NuxtLink>

      <NuxtLink to="/about" class="navbar-item">
        O mnie
      </NuxtLink>

      <NuxtLink to="/about" class="navbar-item">
      	Blog
      </NuxtLink>

      <div class="navbar-item has-dropdown is-hoverable">
        <a class="navbar-link">
		Więcej
        </a>

        <div class="navbar-dropdown">
          <a class="navbar-item">
            Projekty
          </a>
          <a class="navbar-item">
            Produkty 
          </a>
          <a class="navbar-item">
            Kontakt 
          </a>
          <hr class="navbar-divider">
          <a class="navbar-item">
		  Zgłoś błąd
          </a>
        </div>
      </div>
    </div>

    <div class="navbar-end">
      <div class="navbar-item">
        <div class="buttons">
          <a class="button is-primary">
            <strong>Zarejestruj</strong>
          </a>
          <a class="button is-light">
		  Zaloguj
          </a>
        </div>
      </div>
    </div>
  </div>
</nav>
</template>
