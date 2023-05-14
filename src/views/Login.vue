<template>
  <v-container>
    <v-row align="center" justify="center">
      <v-col cols="12" sm="10">
        <v-card class="elevation-6 mt-10">
          <v-window v-model="step">
            <!-- start: login card -->
            <v-window-item :value="1">
              <v-row>
                <v-col cols="12" md="6">
                  <v-card-text class="mt-12">
                    <h4 class="text-center">Login in to Your Account</h4>
                    <h6 class="text-center grey--text">
                      Log in to your account so you can continue Create Your
                      Todos.
                    </h6>
                    <v-row align="center" justify="center">
                      <v-col cols="12" sm="8">
                        <v-text-field
                          label="Email"
                          outlined
                          dense
                          color="blue"
                          autocomplete="false"
                          class="mt-16"
                          v-model="Login.uemail"
                          :class="{ error: errors.uemail }"
                        />
                        <span v-if="errors.uemail" style="color: red">{{
                          errors.uemail
                        }}</span>
                        <v-text-field
                          label="Password"
                          outlined
                          dense
                          color="blue"
                          autocomplete="false"
                          type="password"
                          v-model="Login.upassword"
                          :class="{ error: errors.upassword }"
                        />
                        <span v-if="errors.upassword" style="color: red">{{
                          errors.upassword
                        }}</span>
                        <v-row>
                          <v-col cols="12" sm="7">
                            <v-checkbox
                              label="Remember Me"
                              class="mt-n1"
                              color="blue"
                            >
                            </v-checkbox>
                          </v-col>
                          <v-col cols="12" sm="5">
                            <span class="caption blue--text"
                              >Forgot password</span
                            >
                          </v-col>
                        </v-row>
                        <v-btn @click="SignIn" color="blue" dark block tile
                          >Log in</v-btn
                        >

                        <h5 class="text-center grey--text mt-4 mb-3">
                          Or Log in using
                        </h5>
                        <div
                          class="d-flex justify-space-between align-center mx-10 mb-16"
                        >
                          <v-btn depressed outlined color="grey">
                            <v-icon color="red">fab fa-google</v-icon>
                          </v-btn>
                          <v-btn depressed outlined color="grey">
                            <v-icon color="blue">fab fa-facebook-f</v-icon>
                          </v-btn>
                          <v-btn depressed outlined color="grey">
                            <v-icon color="light-blue lighten-3"
                              >fab fa-twitter</v-icon
                            >
                          </v-btn>
                        </div>
                      </v-col>
                    </v-row>
                  </v-card-text>
                </v-col>
                <v-col cols="12" md="6" class="blue rounded-bl-xl">
                  <div style="text-align: center; padding: 180px 0">
                    <v-card-text class="white--text">
                      <h3 class="text-center">Don't Have an Account Yet?</h3>
                      <h6 class="text-center">
                        Let's get you all set up so you can start creating your
                        your first<br />
                        onboarding experience
                      </h6>
                    </v-card-text>
                    <div class="text-center">
                      <v-btn tile outlined dark @click="step++">SIGN UP</v-btn>
                    </div>
                  </div>
                </v-col>
              </v-row>
            </v-window-item>
            <!-- end: login card -->
            <!-- start : Signup -->
            <v-window-item :value="2">
              <v-row>
                <v-col cols="12" md="6" class="blue rounded-br-xl">
                  <div style="text-align: center; padding: 180px 0">
                    <v-card-text class="white--text">
                      <h3 class="text-center">Alredy Signed up?</h3>
                      <h6 class="text-center">
                        Log in to your account so you can continue <br />
                        Create Your Todos.
                      </h6>
                    </v-card-text>
                    <div class="text-center">
                      <v-btn tile outlined dark @click="step--">Log in</v-btn>
                    </div>
                  </div>
                </v-col>

                <v-col cols="12" md="6">
                  <v-card-text class="mt-12">
                    <h4 class="text-center">Sign Up for an Account</h4>
                    <h6 class="text-center grey--text">
                      Let's get you all set up so you can start creatin your
                      <br />
                      first onboarding experiance
                    </h6>
                    <v-row align="center" justify="center">
                      <v-col cols="12" sm="8">
                        <v-text-field
                          label="Email"
                          outlined
                          dense
                          color="blue"
                          autocomplete="false"
                          v-model="SignUp.email"
                          :class="{ error: errors.email }"
                        />
                        <span v-if="errors.email" style="color: red">{{
                          errors.email
                        }}</span>
                        <v-text-field
                          label="Password"
                          outlined
                          dense
                          color="blue"
                          autocomplete="false"
                          type="password"
                          v-model="SignUp.password"
                          :class="{ error: errors.password }"
                        />
                        <span v-if="errors.password" style="color: red">{{
                          errors.password
                        }}</span>
                        <v-text-field
                          label="Confirm Password"
                          outlined
                          dense
                          color="blue"
                          autocomplete="false"
                          type="password"
                          v-model="SignUp.Cpassword"
                          :class="{ error: errors.Cpassword }"
                        />
                        <span v-if="errors.Cpassword" style="color: red">{{
                          errors.Cpassword
                        }}</span>
                        <span v-if="errors.passwordsMatch" style="color: red">{{
                          errors.passwordsMatch
                        }}</span>
                        <v-row>
                          <v-col cols="12" sm="7">
                            <v-checkbox
                              label="I Accept "
                              class="mt-n1"
                              color="blue"
                            >
                            </v-checkbox>
                          </v-col>
                          <v-col cols="12" sm="5">
                            <span class="caption blue--text ml-n4"
                              >Terms &Conditions</span
                            >
                          </v-col>
                        </v-row>
                        <v-btn @click="Signup" color="blue" dark block tile
                          >Sign up</v-btn
                        >

                        <h5 class="text-center grey--text mt-4 mb-3">
                          Or Sign up using
                        </h5>
                        <div
                          class="d-flex justify-space-between align-center mx-10 mb-11"
                        >
                          <v-btn depressed outlined color="grey">
                            <v-icon color="red">fab fa-google</v-icon>
                          </v-btn>
                          <v-btn depressed outlined color="grey">
                            <v-icon color="blue">fab fa-facebook-f</v-icon>
                          </v-btn>
                          <v-btn depressed outlined color="grey">
                            <v-icon color="light-blue lighten-3"
                              >fab fa-twitter</v-icon
                            >
                          </v-btn>
                        </div>
                      </v-col>
                    </v-row>
                  </v-card-text>
                </v-col>
              </v-row>
            </v-window-item>
            <!-- end : signup -->
          </v-window>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "Login",
  data: () => ({
    step: 1,
    token: "",
    SignUp: {
      email: "",
      password: "",
      Cpassword: "",
    },
    Login: {
      uemail: "",
      upassword: "",
    },
    errors: {},
  }),
  mounted() {
    this.token = localStorage.getItem("user");
    console.log(this.token);
    if (this.token) {
      this.$router.push({ path: "/createtodo" });
    }
  },
  methods: {
    Signup() {
      this.errors = {};
      console.log(
        this.SignUp.email,
        this.SignUp.password,
        this.SignUp.Cpassword
      );

      if (!this.SignUp.email) {
        this.errors.email = "Please enter email.";
      }
      if (!this.SignUp.password) {
        this.errors.password = "Please enter Password.";
      }
      if (!this.SignUp.Cpassword) {
        this.errors.Cpassword = "Please enter Confirm password.";
      }
      if (this.SignUp.password !== this.SignUp.Cpassword) {
        this.errors.passwordsMatch = "Passwords do not match.";
      }

      if (Object.keys(this.errors).length == 0) {
        var myHeaders = new Headers();
        myHeaders.append("Accept", "application/json");

        var formdata = new FormData();
        formdata.append("email", this.SignUp.email);
        formdata.append("password", this.SignUp.password);
        formdata.append("password_confirmation", this.SignUp.Cpassword);

        var requestOptions = {
          method: "POST",
          headers: myHeaders,
          body: formdata,
          redirect: "follow",
        };

        fetch("http://3.232.244.22/api/register", requestOptions)
          .then((response) => response.json())
          .then((result) => {
            let abc = JSON.parse(JSON.stringify(result));

            console.log(abc);

            if (abc.success == true) {
              window.Swal.fire({
                iconColor: "Green",
                icon: "success",
                title: "Success!",
                text: "User Registration successfull.",
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
                text: "The email has already been taken.",
                confirmButtonColor: "red",
                confirmButtonText: "OK",
              });
            }
          })
          .catch((error) => console.log("error", error));
        //   .then((response) => response.text())
        //   .then((result) => console.log(result))
        //   .catch((error) => console.log("error", error));
      }
      //   else {
      //     alert("please fill All Fields");
      //   }
    },
    SignIn() {
      this.errors = {};
      console.log(this.Login.uemail, this.Login.upassword);

      if (!this.Login.uemail) {
        this.errors.uemail = "Please enter email.";
      }
      if (!this.Login.upassword) {
        this.errors.upassword = "Please enter Password.";
      }

      if (Object.keys(this.errors).length == 0) {
        var myHeaders = new Headers();
        myHeaders.append("Accept", "application/json");

        var formdata = new FormData();
        formdata.append("email", this.Login.uemail);
        formdata.append("password", this.Login.upassword);

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

        fetch("http://3.232.244.22/api/login", requestOptions)
          .then((response) => response.json())
          .then((result) => {
            let abc = JSON.parse(JSON.stringify(result));

            console.log(abc);

            if (abc.success === true) {
              localStorage.setItem("user", abc.user.token);
              this.$router.push({ path: "/" });
            } else {
              window.Swal.fire({
                icon: "error",
                title: "Error!",
                text: "Invalid Credentials",
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
      }
    },
  },
  props: {
    source: String,
  },
};
</script>
<style scoped>
.v-application .rounded-bl-xl {
  border-bottom-left-radius: 300px !important;
}
.v-application .rounded-br-xl {
  border-bottom-right-radius: 300px !important;
}
</style>
