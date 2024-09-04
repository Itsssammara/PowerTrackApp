<template>
  <div class="custom-background">
    <navigation />
    <router-view />
    <Footer/>
  </div>
</template>

<script>
import navigation from '@/components/navigation.vue';
import Footer from '@/components/footer.vue';

export default {
  name: 'HomeView',
  components: {
    navigation,
    Footer
  },
};
</script>

<style scoped>
.custom-background {
  background-image: url('https://i.ibb.co/17VgCPP/powrtrackpic.png');
  background-size: cover; 
  background-position: center;
  height: 100vh; 
}

/* Uncomment and fix styles if needed */
/* 
nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
} 
*/
</style>
