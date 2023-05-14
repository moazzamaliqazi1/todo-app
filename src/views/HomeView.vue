<template>
  <v-app>
    <!-- start -->
    <Navbar></Navbar>
    <!-- end -->
    <v-container>
      <v-card class="mx-auto rounded-xl mt-5" flat>
        <v-img src="../assets/banner4.jpg" max-height="100%" max-width="100%">
          <v-card-title class="top ml-10">
            <h2 class="title1 white--text mt-5">Everyone</h2>
          </v-card-title>
          <v-card-title class="top ml-10 mt-n8">
            <h2 class="title2 white--text">Love's Write</h2>
          </v-card-title>
        </v-img>
      </v-card>
    </v-container>
  </v-app>
</template>

<script>
import Navbar from "../components/Navbar.vue";
export default {
  name: "Home",

  components: {
    Navbar,
  },
};
</script>
