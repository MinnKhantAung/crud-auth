<template>
  <div class="container font2 fw-bold">
    <div v-if="error" class="alert alert-danger" role="alert">
        {{ error }}
      </div>
    <form @submit.prevent="signin">
      <div>
        <h3>SignIn...</h3>
        <label for="exampleInputEmail1" class="form-label">Email address</label>
        <input
          type="email"
          class="form-control"
          id="exampleInputEmail1"
          autocomplete="none"
          v-model="user.email"
          required
        />
      </div>
      <div class="mb-3">
        <label for="exampleInputPassword1" class="form-label">Password</label>
        <input
          type="password"
          class="form-control"
          id="exampleInputPassword1"
          autocomplete="none"
          v-model="user.password"
          required
        />
      </div>
      <button v-if="!check" type="submit" class="btn btn-primary">SignIn</button>

      <button v-else class="btn btn-primary" type="button" disabled>
        <span class="spinner-border spinner-border-sm" role="status" aria-hidden="true"></span>
        SignIn...
      </button>

    </form>
  </div>
</template>

<script>
import { ref } from "@vue/reactivity";
import { app } from "../assets/firebase/firebase";
import { getAuth, signInWithEmailAndPassword } from "firebase/auth";
export default {
  emits: ["sign"],
  setup(props, { emit }) {
    const user = ref({
      email: "",
      password: "",
    });
    const error = ref("");
    const check = ref(false);

    function signin() {
      check.value = true;
      const auth = getAuth(app);
      signInWithEmailAndPassword(auth, user.value.email, user.value.password)
        .then(() => {
          emit("sign");
          check.value = false;
        })
        .catch((err) => {
          const errorCode = err.code;
          const errorMessage = err.message;
          error.value = errorMessage;
          check.value = false;
        });
    }
    return { user, check, signin, error };
  },
};
</script>

<style>
</style>