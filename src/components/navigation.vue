<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <div class="container">

        <!-- Toggler/collapsible button -->
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent"
          aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>

        <!-- Navbar links -->
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav ms-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <router-link :to="{ name: 'Home' }" class="nav-link">HOME</router-link>
            </li>
            <li class="nav-item">
              <router-link :to="{ name: 'Energy' }" class="nav-link">ENERGY DATA</router-link>
            </li>
            <li class="nav-item">
              <router-link :to="{ name: 'Reports' }" class="nav-link">REPORTS</router-link>
            </li>
            <li class="nav-item">
              <router-link :to="{ name: 'Help' }" class="nav-link">HELP</router-link>
            </li>
            <li class="nav-item">
              <router-link :to="{ name: 'Login' }" class="nav-link">LOGIN</router-link>
            </li>
            <li class="nav-item">
              <router-link :to="{ name: 'Sign Up' }" class="nav-link">SIGN UP</router-link>
            </li>
            <li class="nav-item">
              <router-link :to="{ name: 'Contact' }" class="nav-link">CONTACT</router-link>
            </li>
          </ul>
        </div>
      </div>
    </nav>
    <router-view/>
  </div>
</template>


<style scoped>
.navbar {
  padding: 10px;
  text-align: center;
}

.nav-link {
  color: rgb(255, 255, 255);
  margin: 0 10px;
  padding: 5px 10px;
  font-family: Radio Canada Big;
}

.nav-item {
  height: 30px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.nav-link:hover,
.router-link-active {
  border-bottom: 2px solid #00FF89;
}

@media screen and (max-width: 420px) {
  .nav-item {
    margin: 10px;
  }
}
</style>
