<template>
  <div class="font2">
    <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
      <div class="container-fluid mx-1">
        <a class="navbar-brand" href="#">Admin</a>

        <div class="d-flex ms-auto">
          <span class="text-light" v-if="CurrentName">
            <small>Log in As</small> {{CurrentName}}
          </span>
        </div>
      </div>
    </nav>
    <!-- end of nav -->
    <div class="mt-3 mx-2">
      <h3 class="mx-3 font1">Activities</h3>
      <div class="row mx-2">
        <div class="col-md-4 my-2">
          <div class="card border-primary" style="height: 200px">
            <div class="card-body text-center">
              <h5 class="card-title fw-bold">Number of Adding Users</h5>
              <h3 class="card-text text-center mt-5">10</h3>
            </div>
          </div>
        </div>
        <div class="col-md-4 my-2">
          <div class="card border-primary" style="height: 200px">
            <div class="card-body text-center">
              <h5 class="card-title fw-bold">Number of Edit Users</h5>
              <h3 class="card-text text-center mt-5">11</h3>
            </div>
          </div>
        </div>
        <div class="col-md-4 my-2">
          <div class="card border-primary" style="height: 200px">
            <div class="card-body text-center">
              <h5 class="card-title fw-bold">Number of Delete Users</h5>
              <h3 class="card-text text-center mt-5">10</h3>
            </div>
          </div>
        </div>
      </div>
      <div class="alert alert-info mx-4 mt-3" role="alert">
        <span><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" class="bi bi-exclamation-triangle-fill flex-shrink-0 me-2" viewBox="0 0 16 16" role="img" aria-label="Warning:">
    <path d="M8.982 1.566a1.13 1.13 0 0 0-1.96 0L.165 13.233c-.457.778.091 1.767.98 1.767h13.713c.889 0 1.438-.99.98-1.767L8.982 1.566zM8 5c.535 0 .954.462.9.995l-.35 3.507a.552.552 0 0 1-1.1 0L7.1 5.995A.905.905 0 0 1 8 5zm.002 6a1 1 0 1 1 0 2 1 1 0 0 1 0-2z"/>
  </svg></span>
  <span>New Version of admin channel Here.</span>
</div>
    </div>
    <!-- end of activities -->
  </div>
</template>

<script>
import { app } from "../assets/firebase/firebase";
import { getAuth, updateProfile } from "firebase/auth";
import { onMounted, ref } from '@vue/runtime-core';
export default {
  setup(){
    const CurrentName = ref();
    onMounted(()=>{
      const auth = getAuth(app);
      const user = auth.currentUser;
      if(user){
        
        CurrentName.value = user.displayName;
      }
      else{
        console.log("llfff");
      }
    })
    return{
      CurrentName
    }
  }
};
</script>

<style>
</style>