<template>
  <v-app>
    <!-- start -->
    <Navbar></Navbar>
    <!-- end -->

    <v-carousel
      cycle
      height="500"
      hide-delimiter-background
      show-arrows-on-hover
      class="mt-12 container"
    >
      <template v-slot:prev="{ on, attrs }">
        <v-btn color="success" v-bind="attrs" v-on="on"
          ><i class="fa-solid fa-backward"></i
        ></v-btn>
      </template>
      <template v-slot:next="{ on, attrs }">
        <v-btn color="info" v-bind="attrs" v-on="on"
          ><i class="fa-solid fa-forward"></i
        ></v-btn>
      </template>
      <v-carousel-item v-for="(item, i) in items" :key="i" :src="item.src">
      </v-carousel-item>
    </v-carousel>
    <div class="text-center p-5">
      <h4>Welcome To My Todo App</h4>
    </div>
    <Footer></Footer>
  </v-app>
</template>

<script>
import Navbar from "../components/Navbar.vue";
import Footer from "../components/Footer.vue";
export default {
  name: "Home",

  components: {
    Navbar,
    Footer,
  },
  data() {
    return {
      items: [
        {
          src: "https://cdn.vuetifyjs.com/images/carousel/sky.jpg",
        },
        {
          src: "https://cdn.vuetifyjs.com/images/carousel/bird.jpg",
        },
        {
          src: "https://cdn.vuetifyjs.com/images/carousel/planet.jpg",
        },
      ],
    };
  },
};
</script>
