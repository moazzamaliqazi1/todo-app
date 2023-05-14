<template>
  <nav
    class="navbar navbar-expand-lg navbar-dark fixed-top"
    style="height: 60px; background-color: #2196f3"
  >
    <div class="container">
      <a class="navbar-brand" href="#">
        <img
          src="https://i.imgur.com/PSXxjNY.png"
          alt=""
          width="35"
          class="rounded-circle"
        />
      </a>

      <div class="navbar-collapse">
        <div class="navbar-nav me-auto">
          <router-link
            to="/"
            class="nav-link active"
            aria-current="page"
            href="#"
            >Home</router-link
          >
          <a class="nav-link active" aria-current="page" href="#">Services</a>
          <a class="nav-link active" aria-current="page" href="#">About</a>
          <a class="nav-link active" aria-current="page" href="#">Contact</a>
          <router-link
            to="/CreateTodo"
            class="nav-link active"
            aria-current="page"
            >Your Todos</router-link
          >
        </div>
        <form class="d-flex">
          <div class="rounded-pill bg-light d-flex">
            <input
              type="text"
              class="form-control rounded-pill border-0 outiline-0 bg-transparent shadow-none py-1"
              placeholder="Search..."
              aria-label="Search ..."
            />
            <span class="pe-2 pt-1 pb-1">
              <i class="fas fa-search text-muted"></i>
            </span>
          </div>
        </form>
        <v-btn
          v-if="isLogin"
          @click="Logout"
          elevation="4"
          small
          rounded
          class="ml-5"
          >Logout</v-btn
        >
        <router-link
          v-if="!isLogin"
          to="/Login"
          class="nav-link active text-white ms-5"
          style="text-decoration: underline"
          aria-current="page"
          >SignIn</router-link
        >
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: "Navbar",
  data: () => ({
    isLogin: false,
    token: "",
  }),
  mounted() {
    this.token = localStorage.getItem("user");
    if (!this.token) {
      this.isLogin = false;
    } else {
      this.isLogin = true;
    }
  },
  methods: {
    Logout() {
      var myHeaders = new Headers();
      myHeaders.append("Accept", "application/json");

      var formdata = new FormData();
      formdata.append("token", this.token);

      var requestOptions = {
        method: "POST",
        headers: myHeaders,
        body: formdata,
        redirect: "follow",
      };

      let loader = window.Swal.fire({
        title: "Please wait",
        html: "Signing Out...",
        allowEscapeKey: false,
        allowOutsideClick: false,
        didOpen: () => {
          window.Swal.showLoading();
        },
      });
      fetch("http://3.232.244.22/api/logout", requestOptions)
        .then((response) => response.json())
        .then((result) => {
          let abc = JSON.parse(JSON.stringify(result));

          console.log(abc);

          if (abc.success === true) {
            // Remove item from localStorage
            localStorage.removeItem("user");

            this.$router.push({ path: "/login" });
          }
        })
        .catch((error) => console.log("error", error))
        .finally(() => {
          loader.close();
        });
    },
  },
};
</script>
