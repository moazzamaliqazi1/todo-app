<template>
  <v-app>
    <!-- start -->
    <Navbar></Navbar>
    <!-- end -->
    <v-container class="mt-15">
      <v-card>
        <v-toolbar style="background-color: #2196f3" class="text-white"
          >Edit Your Todo</v-toolbar
        >
        <v-card-text>
          <v-text-field
            label="Title"
            v-model="item.title"
            variant="underlined"
            disabled
          ></v-text-field>
          <v-textarea
            label="Description"
            v-model="item.description"
            variant="outlined"
          ></v-textarea>
        </v-card-text>
        <v-card-actions class="justify-end">
          <v-btn
            text
            @click="EditTodo"
            style="background-color: #2196f3; color: white"
            elevation="2"
            small
            >Submit</v-btn
          >
        </v-card-actions>
      </v-card>
    </v-container>
    <Footer></Footer>
  </v-app>
</template>

<script>
import Navbar from "../components/Navbar.vue";
import Footer from "../components/Footer.vue";
export default {
  name: "EditTodo",
  components: {
    Navbar,
    Footer,
  },
  data: () => ({
    item: {
      title: "",
      description: "",
    },
    token: "",
    TodoItems: [],
  }),
  mounted() {
    this.token = localStorage.getItem("user");
    console.log(this.token);
    if (!this.token) {
      this.$router.push({ name: "login" });
    }
    console.log(this.$route.params.id);

    // prefill data

    var myHeaders = new Headers();
    myHeaders.append("Accept", "application/json");
    myHeaders.append("Authorization", "Bearer" + this.token);

    var requestOptions = {
      method: "GET",
      headers: myHeaders,
      redirect: "follow",
    };

    fetch(
      "http://3.232.244.22/api/item/" + this.$route.params.id,
      requestOptions
    )
      .then((response) => {
        console.log(response); // Log the response to examine its contents
        return response.json();
      })
      .then((result) => {
        this.item = JSON.parse(JSON.stringify(result.item));
        console.log(this.item);
      })
      .catch((error) => console.log("error", error));
  },
  methods: {
    EditTodo() {
      console.log(this.item.title, this.item.description);

      //   update
      if (this.item.description) {
        // Both fields are filled, proceed with submission
        var myHeaders = new Headers();
        myHeaders.append("Accept", "application/json");
        myHeaders.append("Content-Type", "application/json");
        myHeaders.append("Authorization", "Bearer " + this.token);

        var raw = JSON.stringify({
          description: this.item.description,
        });

        var requestOptions = {
          method: "PUT",
          headers: myHeaders,
          body: raw,
          redirect: "follow",
        };

        let loader = window.Swal.fire({
          title: "Please wait",
          html: "Processing...",
          allowEscapeKey: false,
          allowOutsideClick: false,
          didOpen: () => {
            window.Swal.showLoading();
          },
        });

        fetch(
          "http://3.232.244.22/api/item/" + this.$route.params.id,
          requestOptions
        )
          .then((response) => response.json())
          .then((result) => {
            let abc = JSON.parse(JSON.stringify(result));

            console.log(abc);

            if (abc.success === true) {
              window.Swal.fire({
                iconColor: "Green",
                icon: "success",
                title: "Success!",
                text: "Todo Updated successfull.",
                confirmButtonColor: "Green",
                confirmButtonText: "OK",
                showConfirmButton: true,
                allowOutsideClick: false,
              }).then((result) => {
                if (result.isConfirmed) {
                  this.$router.push({ path: "/createtodo" });
                }
              });
            } else {
              window.Swal.fire({
                icon: "error",
                title: "Error!",
                text: "Unauthenticated",
                confirmButtonColor: "red",
                confirmButtonText: "OK",
              });
            }
          })
          .catch((error) => console.log("error", error))
          .finally(() => {
            loader.close();
          });
      } else {
        // Show error message or handle the case when one or both fields are empty
        window.Swal.fire({
          icon: "error",
          title: "Error!",
          text: "Please Enter Your Todo Data",
          confirmButtonColor: "red",
          confirmButtonText: "OK",
        });
      }
    },
  },
};
</script>
