<template>
  <div>
    <div class="container font2 fw-bold">
      <div v-if="error" class="alert alert-danger" role="alert">
        {{ error }}
      </div>
      <form @submit.prevent="signup">
        <div>
          <h3>SignUp....</h3>
          <label class="form-label">Name</label>
          <input
            type="text"
            class="form-control"
            autocomplete="none"
            required
            :class="{ borderdanger: wrongName }"
            v-model="user.name"
          />
          <label for="exampleInputEmail1" class="form-label"
            >Email address</label
          >
          <input
            type="email"
            class="form-control"
            id="exampleInputEmail1"
            aria-describedby="emailHelp"
            autocomplete="none"
            required
            :class="{ borderdanger: wrongEmail }"
            v-model="user.email"
          />
          <div id="emailHelp" class="form-text d-none d-lg-block">
            <small class="text-muted">
              We'll never share your email with anyone else.</small
            >
          </div>
        </div>
        <div class="mb-3">
          <label for="exampleInputPassword1" class="form-label">Password</label>
          <input
            type="password"
            class="form-control"
            id="exampleInputPassword1"
            autocomplete="none"
            required
            v-model="user.password"
            :class="{ borderdanger: wrongPass }"
          />
        </div>
        <div class="mb-3">
          <label for="exampleInputPassword1" class="form-label"
            >Retype-Password</label
          >
          <input
            type="password"
            class="form-control"
            id="exampleInputPassword2"
            autocomplete="none"
            :class="{ borderdanger: wrongPass }"
            v-model="retype"
          />
        </div>

        <button v-if="!check" type="submit" class="btn btn-primary">
          SignUp
        </button>

        <button v-else class="btn btn-primary" type="button" disabled>
          <span
            class="spinner-border spinner-border-sm"
            role="status"
            aria-hidden="true"
          ></span>
          SignUp...
        </button>
      </form>
    </div>
  </div>
</template>

<script>
import { ref } from "@vue/reactivity";
import { app } from "../assets/firebase/firebase";
import {
  getAuth,
  createUserWithEmailAndPassword,
  updateProfile,
} from "firebase/auth";

export default {
  emits: ["sign"],
  setup(props, { emit }) {
    const user = ref({
      name: "",
      email: "",
      password: "",
    });
    const retype = ref("");
    const error = ref("");
    const wrongPass = ref(false);
    const wrongEmail = ref(false);
    const wrongName = ref(false);
    const check = ref(false);

    function signup() {
      check.value = true;
      if (
        user.value.password.length >= 8 &&
        user.value.password === retype.value
      ) {
        wrongPass.value = false;
        if (user.value.name.length <= 15) {
          wrongName.value = false;
          if (user.value.email.length < 30) {
            wrongEmail.value = false;
            const auth = getAuth(app);
            createUserWithEmailAndPassword(
              auth,
              user.value.email,
              user.value.password
            )
              .then(() => {
                updateProfile(auth.currentUser, {
                  displayName: user.value.name,
                });
                emit("sign");
                check.value = false;
                console.log(auth.currentUser);
              })
              .catch((err) => {
                const errorCode = err.code;
                const errorMessage = err.message;
                error.value = errorMessage;
                check.value = false;
                // ..
              });
          } else {
            wrongEmail.value = true;
            check.value = false;
            error.value = "Email is too long";
          }
        } else {
          wrongName.value = true;
          check.value = false;
          error.value = "Your name is too long";
        }
      } else {
        wrongPass.value = true;
        check.value = false;
        error.value =
          "Password and Retype Password must equal and Password must be at least 8 character long";
      }
    }
    return {
      signup,
      user,
      retype,
      error,
      wrongPass,
      wrongEmail,
      wrongName,
      check,
    };
  },
};
</script>

<style>
.borderdanger {
  border: solid 2px red;
}
</style>