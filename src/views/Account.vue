<template>
  <div class="fw-bold p-3 m-3">
    <div >
      <div class="d-flex justify-content-between">
        <div>
          <h3 class="font1">Account Setting</h3>
        </div>
        <div class="me-4" v-if="tog">
          <span class="link" @click="toggle"
            ><svg
              xmlns="http://www.w3.org/2000/svg"
              width="26"
              height="26"
              fill="currentColor"
              class="bi bi-pencil-fill"
              viewBox="0 0 16 16"
            >
              <path
                d="M12.854.146a.5.5 0 0 0-.707 0L10.5 1.793 14.207 5.5l1.647-1.646a.5.5 0 0 0 0-.708l-3-3zm.646 6.061L9.793 2.5 3.293 9H3.5a.5.5 0 0 1 .5.5v.5h.5a.5.5 0 0 1 .5.5v.5h.5a.5.5 0 0 1 .5.5v.5h.5a.5.5 0 0 1 .5.5v.207l6.5-6.5zm-7.468 7.468A.5.5 0 0 1 6 13.5V13h-.5a.5.5 0 0 1-.5-.5V12h-.5a.5.5 0 0 1-.5-.5V11h-.5a.5.5 0 0 1-.5-.5V10h-.5a.499.499 0 0 1-.175-.032l-.179.178a.5.5 0 0 0-.11.168l-2 5a.5.5 0 0 0 .65.65l5-2a.5.5 0 0 0 .168-.11l.178-.178z"
              /></svg
          ></span>
        </div>
      </div>
      <table class="table table-borderless table-responsive my-3">
        <tbody>
          <tr>
            <td>Name</td>
            <td>:</td>
            <td>
              <span v-if="show">{{ CurrentName }}</span
              ><span v-else><input type="text" v-model="CurrentName" /></span>
            </td>
          </tr>
          <tr>
            <td>Email</td>
            <td>:</td>
            <td>
              <span>{{ CurrentMail }}</span
              >
            </td>
          </tr>
        </tbody>
      </table>
      <div v-if="!show">
        <button class="btn btn-primary" @click="edit">Edit</button>
        <button class="btn btn-danger mx-2" @click="cancel">Cancel</button>
      </div>
      <div class="mt-5">
        <p>
          Created at
          ( <span >{{ CreateTime }}</span> )
        </p>
        <p>
          Last SignIn at
          ( <span>{{ LastLogin }}</span> )
        </p>
      </div>
      
    </div>
  </div>
</template>

<script>
import { ref } from "@vue/reactivity";
import { onMounted, watch } from "@vue/runtime-core";
import { app } from "../assets/firebase/firebase";
import { getAuth, updateProfile } from "firebase/auth";
export default {
  setup() {
    const CurrentName = ref();
    const CurrentMail = ref();
    const CurrentPhone = ref();
    const CreateTime = ref();
    const LastLogin = ref();
    const tog = ref(true);
    const show = ref("true");
    

     function edit() {
      const auth =  getAuth(app);
      const user =  auth.currentUser;
      updateProfile(user, {
        displayName: CurrentName.value,
        email:CurrentMail.value,
        phoneNumber: CurrentPhone.value
      });
      console.log(user);
      const authd =  getAuth(app);
      const cuser = authd.currentUser;
      if (cuser) {
        CurrentName.value = cuser.displayName;
        CurrentMail.value = cuser.email;
        CurrentPhone.value = cuser.phoneNumber;
      }
      console.log(user.displayName);
      
      show.value = !show.value;
    }
    watch(CurrentName, (currentValue) => {
       const auth =  getAuth(app);
      const user = auth.currentUser;
      user.displayName = currentValue;
    });
    
    function toggle(){
      show.value = !show.value;
      tog.value = false;
    }

    function cancel(){
      show.value = true;
      tog.value = true;
    }

    onMounted(() => {
      const auth = getAuth(app);
      const user = auth.currentUser;

      if (user) {
        CurrentName.value = user.displayName;
        CurrentMail.value = user.email;
        CurrentPhone.value = user.phoneNumber;

        CreateTime.value = user.metadata.creationTime;
        LastLogin.value = user.metadata.lastSignInTime;

        console.log(user);
        // ...
      } else {
        // No user is signed in.
      }
    });
    return {
      CurrentName,
      CurrentPhone,
      CurrentMail,
      CreateTime,
      LastLogin,
      show,
      edit,
      tog,
      toggle,
      cancel
    };
  },
};
</script>

<style>
</style>