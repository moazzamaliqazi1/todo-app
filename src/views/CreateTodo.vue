<template>
  <v-app id="inspire">
    <Navbar></Navbar>
    <!-- navbar: end -->
    <!-- add todo : start -->
    <v-row justify="space-around" style="margin-top: 60px">
      <v-col cols="auto">
        <v-dialog transition="dialog-top-transition" max-width="600">
          <template v-slot:activator="{ on, attrs }">
            <v-btn
              style="background-color: #2196f3"
              class="text-white"
              v-bind="attrs"
              v-on="on"
              rounded
              large
              >+ Add Todo</v-btn
            >
          </template>
          <template v-slot:default="dialog">
            <v-card>
              <v-toolbar style="background-color: #2196f3" dark
                >Add Your Todo</v-toolbar
              >
              <v-card-text>
                <v-text-field
                  label="Title"
                  v-model="title"
                  variant="underlined"
                ></v-text-field>
                <v-textarea
                  label="Description"
                  v-model="des"
                  variant="outlined"
                ></v-textarea>
              </v-card-text>
              <v-card-actions class="justify-end">
                <v-btn text @click="dialog.value = false">Close</v-btn>
                <v-btn
                  text
                  @click="AddTodo"
                  style="background-color: #2196f3; color: white"
                  elevation="2"
                  small
                  >Submit</v-btn
                >
              </v-card-actions>
            </v-card>
          </template>
        </v-dialog>
      </v-col>
    </v-row>
    <!-- add totdo end -->
    <!-- list start -->

    <section class="vh-100 gradient-custom-2 mt-3">
      <div class="container py-5 h-100">
        <div class="row d-flex justify-content-center align-items-center h-100">
          <div class="col-md-12 col-xl-10">
            <div class="card mask-custom">
              <div class="card-body p-4 text-white">
                <div class="text-center pt-3 pb-2">
                  <img
                    src="https://mdbcdn.b-cdn.net/img/Photos/new-templates/bootstrap-todo-list/check1.webp"
                    alt="Check"
                    width="60"
                  />
                  <h2 class="my-4">Task List</h2>
                </div>

                <table
                  id="example"
                  class="table"
                  style="width: 100%"
                  ref="dataTable"
                >
                  <thead>
                    <tr class="text-white">
                      <th scope="col">TITLE</th>
                      <th scope="col">DESCRIPTION</th>
                      <th scope="col">Actions</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr
                      class="fw-normal text-white"
                      v-for="item in TodoItems"
                      :key="item.id"
                    >
                      <th>
                        <p>
                          <span class="ms-2">{{ item.title }}</span>
                        </p>
                      </th>
                      <td class="align-middle">
                        <span>{{ item.description }}</span>
                      </td>
                      <td class="align-middle d-flex gap-2">
                        <!-- edit dialogue start -->
                        <router-link :to="'/edittodo/' + item.id"
                          ><i class="fas fa-edit fa-lg text-white pt-3"></i
                        ></router-link>
                        <!-- end -->
                        <v-btn @click="DeleteTodo(item.id)" icon
                          ><i class="fas fa-trash-alt fa-lg text-warning"></i
                        ></v-btn>
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- list end -->
    <Footer></Footer>
  </v-app>
</template>

<script>
import Navbar from "../components/Navbar.vue";
import Footer from "../components/Footer.vue";
export default {
  name: "CreateTodo",
  components: {
    Navbar,
    Footer,
  },
  data: () => ({
    title: "",
    des: "",
    EditTitle: "",
    EditDes: "",
    token: "",
    TodoItems: [],
  }),
  mounted() {
    this.token = localStorage.getItem("user");
    console.log(this.token);
    if (!this.token) {
      this.$router.push({ name: "login" });
    }
    // get list
    var myHeaders = new Headers();
    myHeaders.append("Accept", "application/json");
    myHeaders.append("Authorization", "Bearer " + this.token);

    var requestOptions = {
      method: "GET",
      headers: myHeaders,
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

    fetch("http://3.232.244.22/api/items", requestOptions)
      .then((response) => {
        console.log(response); // Log the response to examine its contents
        return response.json();
      })
      .then((result) => {
        this.TodoItems = JSON.parse(JSON.stringify(result.items.data));
        console.log(this.TodoItems);
      })
      .catch((error) => console.log("error", error))

      // .then((response) => response.text())
      // .then((result) => console.log(result))
      // .catch((error) => console.log("error", error))
      .finally(() => {
        loader.close();
      });
  },
  methods: {
    AddTodo() {
      if (this.title && this.des) {
        // Both fields are filled, proceed with submission
        console.log(this.token);
        console.log(this.title, this.des);
        var myHeaders = new Headers();
        myHeaders.append("Accept", "application/json");
        myHeaders.append("Authorization", "Bearer" + this.token);

        var formdata = new FormData();
        formdata.append("title", this.title);
        formdata.append("description", this.des);

        var requestOptions = {
          method: "POST",
          headers: myHeaders,
          body: formdata,
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

        fetch("http://3.232.244.22/api/item", requestOptions)
          .then((response) => response.json())
          .then((result) => {
            let abc = JSON.parse(JSON.stringify(result));

            console.log(abc);

            if (abc.success === true) {
              window.Swal.fire({
                iconColor: "Green",
                icon: "success",
                title: "Success!",
                text: "Todo Added successfull.",
                confirmButtonColor: "Green",
                confirmButtonText: "OK",
                showConfirmButton: true,
                allowOutsideClick: false,
              }).then((result) => {
                if (result.isConfirmed) {
                  location.reload();
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
        //   .then((response) => response.text())
        //   .then((result) => console.log(result))
        //   .catch((error) => console.log("error", error));
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
    // delete todo
    DeleteTodo(id) {
      console.log(id);
      var myHeaders = new Headers();
      myHeaders.append("Accept", "application/json");
      myHeaders.append("Authorization", "Bearer " + this.token);

      var requestOptions = {
        method: "DELETE",
        headers: myHeaders,
        redirect: "follow",
      };

      // fetch("http://3.232.244.22/api/item/" + id, requestOptions)
      window.Swal.fire({
        title: "Are you sure?",
        text: "You won't be able to revert this!",
        icon: "warning",
        showCancelButton: true,
        confirmButtonColor: "#de1e07",
        confirmButtonText: "Yes, delete it!",
        cancelButtonText: "No, cancel",
      }).then((result) => {
        if (result.isConfirmed) {
          let loader = window.Swal.fire({
            title: "Please wait",
            html: "Deleting the order...",
            allowEscapeKey: false,
            allowOutsideClick: false,
            didOpen: () => {
              window.Swal.showLoading();
            },
          });
          fetch("http://3.232.244.22/api/item/" + id, requestOptions)
            .then((response) => response.json())
            .then((result) => {
              let abc = JSON.parse(JSON.stringify(result));

              console.log(abc);

              if (abc.success == true) {
                window.Swal.fire({
                  iconColor: "Green",
                  confirmButtonColor: "Green",
                  icon: "success",
                  title: "Success!",
                  text: "Order deleted",
                  confirmButtonText: "OK",
                }).then(() => {
                  location.reload(); // <-- Reloads the page
                });
              } else {
                window.Swal.fire({
                  icon: "error",
                  title: "Error!",
                  text: "Error in delete",
                  confirmButtonText: "OK",
                });
              }
            })
            .catch((error) => console.log("error", error))
            .finally(() => {
              // Close the loader here
              loader.then(() => {
                window.Swal.close();
              });
            });
        } else if (result.dismiss === window.Swal.DismissReason.cancel) {
          window.Swal.fire({
            title: "Cancelled",
            text: "Your order is safe :)",
            icon: "error",
            confirmButtonText: "OK",
          });
        }
      });
    },
  },
};
</script>

<style lang="scss" scoped>
.gradient-custom-2 {
  /* fallback for old browsers */
  background: #7e40f6;

  /* Chrome 10-25, Safari 5.1-6 */
  background: -webkit-linear-gradient(
    to right,
    rgba(126, 64, 246, 1),
    rgba(80, 139, 252, 1)
  );

  /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  background: linear-gradient(to right, #508bfc, #2196f3);
}

.mask-custom {
  background: rgba(24, 24, 16, 0.2);
  border-radius: 2em;
  backdrop-filter: blur(25px);
  border: 2px solid rgba(255, 255, 255, 0.05);
  background-clip: padding-box;
  box-shadow: 10px 10px 10px rgba(46, 54, 68, 0.03);
}
</style>
