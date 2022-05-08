<template>
  <div class="container font2">
    <div id="nav"></div>
    <div class="d-flex justify-content-center">
      <div v-if="!isLogged">
        <div v-if="isSigned" class="border p-4" style="width: 400px">
          <SignIn @sign="isLogged = true"></SignIn>
          <div class="text-center">
            <small
              >Not Have Account?
              <span @click="isSigned = !isSigned" class="text-primary link"
                >SignUp Here</span
              ></small
            >
          </div>
        </div>
        <div v-else class="border p-4" style="width: 400px">
          <SignUp  @sign="isLogged = true"></SignUp>
          <div class="text-center">
            <small
              >Already Have Account?
              <span @click="isSigned = !isSigned" class="text-primary link"
                >SignIn Here</span
              ></small
            >
          </div>
        </div>
      </div>
      <div class="w-100" v-else>
        <div class="row">
          <div class="col-md-2 col-1 text-center">
            <Navbar @sign="isLogged = false"></Navbar>
          </div>
          <div class="col-md-10 col-11 ">
            <router-view @userid="receiveid($event)" :id="id" />
          </div>
        </div>
      </div>
    </div>
    <footer class="bg-dark text-white text-center py-2 mt-5">
      Made with
      <span class="text-danger mx-2"
        ><svg
          xmlns="http://www.w3.org/2000/svg"
          width="16"
          height="16"
          fill="currentColor"
          class="bi bi-heart-fill"
          viewBox="0 0 16 16"
        >
          <path
            fill-rule="evenodd"
            d="M8 1.314C12.438-3.248 23.534 4.735 8 15-7.534 4.736 3.562-3.248 8 1.314z"
          /></svg
      ></span>
    </footer>
  </div>
</template>

<script setup>
import { ref } from "@vue/reactivity";
import SignIn from "./components/SignIn.vue";
import SignUp from "./components/SignUp.vue";
import Navbar from "../src/components/Navbar.vue";

const isLogged = ref(false);
const isSigned = ref(false);
const id = ref("");
function receiveid(i) {
  id.value = i;
  console.log(id.value);
}
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Roboto:ital,wght@1,100&display=swap"); /* #nav a.router-link-exact-active {
  color: #42b983;
} */
@import url("https://fonts.googleapis.com/css2?family=PT+Serif&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Prompt:wght@200&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Anton&display=swap");
.link {
  color: rgb(10, 94, 216);
  cursor: pointer;
  font-weight: bold;
}
.usertable {
  background-color: #d1e7dd;
}

.font1 {
  font-family: "Anton", sans-serif;
}
.font2 {
  font-family: "Prompt", sans-serif;
}
.font3 {
  font-family: "PT Serif", serif;
}
</style>
