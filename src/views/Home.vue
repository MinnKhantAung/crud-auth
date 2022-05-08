<template>
  <div class="container-fluid">
    <Content></Content>
    </div>
</template>

<script>
import Content from '../components/Content'
import { app } from "../assets/firebase/firebase";
import { getAuth } from "firebase/auth";
import Navbar from "../components/Navbar";
import { onMounted, ref } from "@vue/runtime-core";
export default {
  components: {
    Content, Navbar },
  setup() {
    const CurrentUser = ref("");
    const CurrentMail = ref("");



    onMounted(() => {
      const auth = getAuth(app);
      const user = auth.currentUser;

      if (user) {
        CurrentUser.value = user.displayName;
        CurrentMail.value = user.email;
        console.log(user);
        // ...
      } else {
        // No user is signed in.
      }
    });

    return {
    CurrentUser,CurrentMail
    };
  },
};
</script>
