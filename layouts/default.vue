<template>
 <v-app dark class="background"> 
     <top-navbar />   
      <v-main class="background">
        <v-container>
           <Nuxt />
        </v-container>
      </v-main>
      <Footer />
  </v-app>
</template>

<script>
import TopNavbar from "../components/partials/Navbar.vue";
import Footer from "../components/partials/Footer.vue";
export default {
  components: { TopNavbar, Footer },
  data() {
    return {};
  },
};
</script>