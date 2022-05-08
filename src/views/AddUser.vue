<template>
  <div>
      <div class="d-flex justify-content-center bg-white mt-2 mx-4">
    <form @submit.prevent="addUser">
      <div class="form-group mb-3">
        <label for="exampleFormControlInput1">Name:</label>
        <input
          type="text"
          class="form-control mt-2"
          id="exampleFormControlInput1"
          placeholder="Name"
          v-model="user.name"
          required
        />
      </div>
      <div class="form-group mb-3">
        <label for="phone">Phone:</label>
        <input
          type="tel"
          class="form-control mt-2"
          name="phone"
          placeholder="phone no length must be 10"
          v-model="user.phone"
          required
        />
      </div>
      <div class="form-group mb-3">
        <label for="exampleFormControlInput1">Email:</label>
        <input
          type="text"
          class="form-control mt-2"
          id="exampleFormControlInput12"
          placeholder="email"
          v-model="user.email"
          required
          pattern=".+@gmail\.com" size="30" 
        />
      </div>
      <div class="form-group mb-3">
        <label for="exampleFormControlInput1">Age:</label>
        <input
          type="number"
          class="form-control mt-2"
          id="exampleFormControlInput15"
          placeholder="age"
          v-model="user.age"
        />
      </div>
      <div class="form-group mb-3">
        <label for="cars">Job Position:</label>
        <select id="cars" name="cars" class="form-control mt-2" v-model="user.jobposition">
          <option value="Tester">Tester</option>
          <option value="Developer">Developer</option>
          <option value="Designer">Designer</option>
          <option value="HR">HR</option>
        </select>
      </div>
      <button v-if="!check" type="submit" class="my-2 btn btn-primary">AddUser</button>
       <button v-else class="my-2 btn btn-primary" type="button" disabled>
          <span
            class="spinner-border spinner-border-sm"
            role="status"
            aria-hidden="true"
          ></span>
          AddUser
        </button>
        <button class="btn btn-danger ms-2" @click="toBack">Cancel</button>
    </form>
  </div>
  </div>
</template>

<script>
import { ref } from '@vue/reactivity'
import { useRouter } from "vue-router";
import axios from 'axios';
export default {
    setup(){
        const router = useRouter();
        var check = ref(false);
        var user = ref({
            name:"",
            email:"",
            phone:"",
            age:"",
            jobposition:""
        })
        
        function toBack(){
            router.push("/users");
        }
        function addUser(){
            check.value = true;
            if(this.user.age >0 && this.user.age<50 && this.user.phone.length>0 && this.user.phone.length<11){
          axios
        .post("https://testing-api-mock.herokuapp.com/users", {
          fullname: this.user.name,
          phoneNo: this.user.phone,
          email: this.user.email,
          age: this.user.age,
          jobPosition: this.user.jobposition,
        })
        .then(() => {
            check.value= false;
          router.push("/users");
        })
        .catch((error)=>{
            check.value = false;
            console.log(error);
            alert("please carefully add employee")
        })
      }else{
        check.value = false;
          alert("rule:age must be between 10 and 50 and phone no length must be 10")
      }
   
        
 
        }
        return{
            user,
            addUser,
            check,
            toBack
        }
    }
}
</script>

<style>

</style>