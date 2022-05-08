<template>
  <div class="container table-responsive p-3 m-3 font2">
    <h3 class="font1">USERs</h3>
    <!--start modal -->
    <div
        class="modal fade"
        id="exampleModal1"
        tabindex="-1"
        aria-labelledby="exampleModalLabel"
        aria-hidden="true"
      >
        <div class="modal-dialog modal-dialog-centered">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="exampleModalLabel">
                Search User By Name
              </h5>
              <button
                type="button"
                class="btn-close"
                data-bs-dismiss="modal"
                aria-label="Close"
              ></button>
            </div>

            <div class="modal-footer d-flex justify-content-center">
              <input type="text" v-model="con">
              <button class="btn btn-success btn-sm" data-bs-dismiss="modal" @click="search">Search</button>
              
            </div>
          </div>
        </div>
      </div>
    <!-- start of table -->
    <table v-if="show" class="table table-success mt-2 table-hover">
      <thead>
        <tr >
          <td colspan="2">
            
            <span class="d-inline d-lg-none link" data-bs-toggle="modal"
        data-bs-target="#exampleModal1"
              ><svg
                xmlns="http://www.w3.org/2000/svg"
                width="26"
                height="26"
                fill="currentColor"
                class="bi bi-search"
                viewBox="0 0 16 16"
              >
                <path
                  d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z"
                /></svg
            ></span>
            <span class="d-none d-lg-inline">
              <input
                type="text"
                class="rounded p-1 border-info w-25"
                placeholder="Search by Name"
                v-model="con"
              />

              <button class="btn btn-primary btn-sm ms-1" @click="search">
                search
              </button>
            </span>
            <label class="ms-3 me-2"><small>Order by :</small></label>
            <select v-model="order" class="usertable rounded">
              <option value="asc" selected>asc</option>
              <option value="desc">desc</option>
            </select>
          </td>
          <td colspan="2"><button class="btn btn-primary btn-sm w-100" @click="toAddUser">Add</button></td>
        </tr>
        <!-- end of one row -->
        <tr>
          <th scope="col">Name</th>
          <th  scope="col">Email</th>
          <th class="d-none d-md-block" scope="col">Phone</th>
          <th scope="col">Position</th>
        </tr>
        <!-- end of two row and thead -->
      </thead>
      <tbody>
        <tr class="font2 fw-bold" v-for="user in users" :key="user.id" @click="EachUser(user.id)">
          <td>{{ user.fullname }}</td>
          <td>{{ user.email }}</td>
          <td class="d-none d-md-block">{{ user.phoneNo }}</td>
          <td>{{ user.jobPosition }}</td>
        </tr> 
        <!-- end of user data  -->
        <tr>
          <td colspan="2" class="fw-bold">
            <span class="d-none d-md-inline">Page</span> {{ page }} of {{ totalpage }}
            <select
              v-model="position"
              aria-label="Default select example"
              class="ms-3 usertable  rounded"
            >
              <option value="" selected>Select Job</option>
              <option value="Designer">Designer</option>
              <option value="HR">HR</option>
              <option value="Developer">Developer</option>
              <option value="Tester">Tester</option>
            </select>
          </td>
          <td colspan="2" class="text-end  ">
            <span class="link " @click="page--" v-if="page > 1"
              ><svg
                xmlns="http://www.w3.org/2000/svg"
                width="25"
                height="25"
                fill="currentColor"
                class="bi bi-caret-left-fill"
                viewBox="0 0 16 16"
              >
                <path
                  d="m3.86 8.753 5.482 4.796c.646.566 1.658.106 1.658-.753V3.204a1 1 0 0 0-1.659-.753l-5.48 4.796a1 1 0 0 0 0 1.506z"
                /></svg></span
            ><span v-else class=""
              ><svg
                xmlns="http://www.w3.org/2000/svg"
                width="25"
                height="25"
                fill="currentColor"
                class="bi bi-caret-left-fill text-muted"
                viewBox="0 0 16 16"
              >
                <path
                  d="m3.86 8.753 5.482 4.796c.646.566 1.658.106 1.658-.753V3.204a1 1 0 0 0-1.659-.753l-5.48 4.796a1 1 0 0 0 0 1.506z"
                /></svg
            ></span>
            <span class=" link" @click="page++" v-if="page != totalpage"
              ><svg
                xmlns="http://www.w3.org/2000/svg"
                width="25"
                height="25"
                fill="currentColor"
                class="bi bi-caret-right-fill"
                viewBox="0 0 16 16"
              >
                <path
                  d="m12.14 8.753-5.482 4.796c-.646.566-1.658.106-1.658-.753V3.204a1 1 0 0 1 1.659-.753l5.48 4.796a1 1 0 0 1 0 1.506z"
                /></svg
            ></span>
            <span v-else
              ><svg
                xmlns="http://www.w3.org/2000/svg"
                width="25"
                height="25"
                fill="currentColor"
                class="bi bi-caret-right-fill text-muted"
                viewBox="0 0 16 16"
              >
                <path
                  d="m12.14 8.753-5.482 4.796c-.646.566-1.658.106-1.658-.753V3.204a1 1 0 0 1 1.659-.753l5.48 4.796a1 1 0 0 1 0 1.506z"
                /></svg
            ></span>
          </td>
        </tr>
        <!-- end of tabel footer -->
      </tbody>
    </table>
    
    <!-- placeholder table -->
    <PlaceHolderTable v-else></PlaceHolderTable>
    <div>
       <label class="ms-3 me-2 fw-bold d-none d-sm-inline">Optional Setting :</label>
            <select v-model="sort" class="usertable  rounded mb-1">
              <option value="fullname" selected>Sort By Name</option>
              <option value="age">Sort By Age</option>
            </select>
    </div>
    <div class="ms-3 fw-bold">Total User = {{totaluser}}</div>
  </div>
</template>

<script>
import PlaceHolderTable from "../components/PlaceHolderTable";
import { useRouter } from "vue-router";
import { onMounted, ref, watch } from "@vue/runtime-core";
import axios from "axios";
export default {
  components: { PlaceHolderTable },
  setup(props, { emit }) {
    const router = useRouter();
    var users = ref([]);
    var page = ref();
    var totalpage = ref();
    var totaluser = ref();
    var user_api = ref(
      "https://testing-api-mock.herokuapp.com/users?fullname=&email=&phoneNo=&jobPosition=&age=&size=3&sort=fullname:asc&page="
    );
    var show = ref(false);
    var order = ref("asc");
    var con = ref("");
    var position = ref("");
    var sort = ref("fullname")

    watch([order, page, position,sort], (currentValue) => {
      console.log(currentValue);
      show.value = false;
      axios
        .get(
          "https://testing-api-mock.herokuapp.com/users?fullname=&email=&phoneNo=&jobPosition=" +
            currentValue[2] +
            "&age=&page=" +
            currentValue[1] +
            "&size=3&sort="+currentValue[3]+":" +
            currentValue[0]
        )
        .then((response) => {
          totalpage.value = response.data.totalPages;
          page.value = response.data.page;
          users.value = response.data.results;
          show.value = true;

        });
    });
    
    function toAddUser(){
      router.push("/adduser")
    } 
    function search() {
      if (con) {
        show.value = false;
        axios
          .get(
            "https://testing-api-mock.herokuapp.com/users?fullname=" +
              con.value +
              "&email=&phoneNo=&jobPosition=&age=&page=&size=3&sort=fullname:" +
              con.value
          )
          .then((response) => {
            totalpage.value = response.data.totalPages;
            page.value = response.data.page;
            users.value = response.data.results;
            show.value = true;
          });
      }
    }
    function EachUser(e){
      emit("userid",e);
      router.push("/edit/"+e)
    }
    onMounted(() => {
      axios.get(user_api.value + 1).then((response) => {
        console.log(response.data);
        totaluser.value = response.data.totalResults;
        totalpage.value = response.data.totalPages;
        page.value = response.data.page;
        users.value = response.data.results;
        console.log(users);
        show.value = true;
      });
    });

    return {
      users,
      page,
      totalpage,
      show,
      order,
      con,
      search,
      position,
      toAddUser,
      sort,
      EachUser,
      totaluser
    };
  },
};
</script>

<style>
</style>