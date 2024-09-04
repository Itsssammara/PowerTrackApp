<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-dark custom-pink">
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
              <router-link :to="{ name: 'Calculate' }" class="nav-link">CALCULATE</router-link>
            </li>
            <li class="nav-item">
              <router-link :to="{ name: 'Help' }" class="nav-link">HELP</router-link>
            </li>
            <li class="nav-item">
              <router-link :to="{ name: 'Login' }" class="nav-link">LOGIN</router-link>
            </li>
            <li class="nav-item">
              <router-link :to="{ name: 'Contact' }" class="nav-link">CONTACT</router-link>
            </li>
          </ul>
        </div>
      </div>
    </nav>
    <!-- <router-view/> -->
  </div>
</template>

<style scoped>
.navbar {
  padding: 10px;
  text-align: center;
}

.custom-pink {
  background-color: #978909; /* Hot Pink color */
}

.nav-link {
  color: #FFFFFF; /* White text color */
  margin: 0 10px;
  padding: 5px 10px;
  font-family: Radio Canada Big;
  position: relative;
}

.nav-link::after {
  content: '';
  position: absolute;
  left: 0;
  bottom: 0;
  width: 100%;
  height: 2px;
  background-color: #ffffff;
  transform: scaleX(0);
  transform-origin: bottom right;
  transition: transform 0.4s ease-in-out; /* Increased duration and smooth easing */
}

.router-link-active::after {
  transform: scaleX(1);
  transform-origin: bottom left;
}

.nav-item {
  height: 30px;
  display: flex;
  justify-content: center;
  align-items: center;
}

@media screen and (max-width: 420px) {
  .nav-item {
    margin: 10px;
  }
}
</style>
