<template>
  <div class="container-fluid m-4">
    <div v-if="eachuser">
      <div class="d-flex justify-content-between me-5">
        <div><h3>User Details</h3></div>
        <div class="me-5">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="26"
            height="26"
            fill="currentColor"
            class="bi bi-pencil-fill link"
            viewBox="0 0 16 16"
            @click="
              show = !show;
              edit = !edit;
            "
            v-if="!edit"
          >
            <path
              d="M12.854.146a.5.5 0 0 0-.707 0L10.5 1.793 14.207 5.5l1.647-1.646a.5.5 0 0 0 0-.708l-3-3zm.646 6.061L9.793 2.5 3.293 9H3.5a.5.5 0 0 1 .5.5v.5h.5a.5.5 0 0 1 .5.5v.5h.5a.5.5 0 0 1 .5.5v.5h.5a.5.5 0 0 1 .5.5v.207l6.5-6.5zm-7.468 7.468A.5.5 0 0 1 6 13.5V13h-.5a.5.5 0 0 1-.5-.5V12h-.5a.5.5 0 0 1-.5-.5V11h-.5a.5.5 0 0 1-.5-.5V10h-.5a.499.499 0 0 1-.175-.032l-.179.178a.5.5 0 0 0-.11.168l-2 5a.5.5 0 0 0 .65.65l5-2a.5.5 0 0 0 .168-.11l.178-.178z"
            />
          </svg>
        </div>
      </div>
      <table class="table table-borderless table-responsive my-3">
        <tbody>
          <tr>
            <td>Name</td>
            <td>:</td>
            <td>
              <span v-if="show">{{ eachuser.fullname }}</span
              ><span v-else
                ><input type="text" v-model="eachuser.fullname"
              /></span>
            </td>
          </tr>
          <tr>
            <td>Email</td>
            <td>:</td>
            <td>
              <span v-if="show">{{ eachuser.email }}</span
              ><span v-else
                ><input type="text" v-model="eachuser.email"
              /></span>
            </td>
          </tr>
          <tr>
            <td>Phone Number</td>
            <td>:</td>
            <td>
              <span v-if="show">{{ eachuser.phoneNo }}</span
              ><span v-else
                ><input type="text" v-model="eachuser.phoneNo"
              /></span>
            </td>
          </tr>
          <tr>
            <td>Age</td>
            <td>:</td>
            <td>
              <span v-if="show">{{ eachuser.age }}</span
              ><span v-else><input type="text" v-model="eachuser.age" /></span>
            </td>
          </tr>
          <tr>
            <td>Position</td>
            <td>:</td>
            <td>
              <span v-if="show">{{ eachuser.jobPosition }}</span
              ><span v-else>
                <select v-model="eachuser.jobPosition">
                  <option value="Tester">Tester</option>
                  <option value="Developer">Developer</option>
                  <option value="Designer">Designer</option>
                  <option value="HR">HR</option>
                </select>
              </span>
            </td>
          </tr>
        </tbody>
      </table>
      <div v-if="!show">
        <button v-if="del" class="btn btn-primary mx-2" @click="editfunc">Edit</button>
        <button v-else class="btn btn-primary mx-2" type="button" disabled>
                <span
                  class="spinner-border spinner-border-sm"
                  role="status"
                  aria-hidden="true"
                ></span>
                Edit
              </button>
        <button
          class="btn btn-danger"
          @click="
            show = true;
            edit = false;
          "
        >
          Cancel
        </button>
      </div>

      <div
        class="modal fade"
        id="exampleModal3"
        tabindex="-1"
        aria-labelledby="exampleModalLabel"
        aria-hidden="true"
      >
        <div class="modal-dialog modal-dialog-centered">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="exampleModalLabel">
                Are You Sure to Delete "{{ eachuser.fullname }}"?
              </h5>
              <button
                type="button"
                class="btn-close"
                data-bs-dismiss="modal"
                aria-label="Close"
              ></button>
            </div>

            <div class="modal-footer">
              <button
                v-if="del"
                type="button"
                @click="deluser"
                data-bs-dismiss="modal"
                class="btn btn-primary"
              >
                Delete
              </button>

              <button v-else class="btn btn-primary" type="button" disabled>
                <span
                  class="spinner-border spinner-border-sm"
                  role="status"
                  aria-hidden="true"
                ></span>
                Delete
              </button>
              <button
                type="button"
                class="btn btn-danger"
                data-bs-dismiss="modal"
              >
                Cancel
              </button>
            </div>
          </div>
        </div>
      </div>

      <div
        v-if="show"
        class="text-end me-5"
        data-bs-toggle="modal"
        data-bs-target="#exampleModal3"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="26"
          height="26"
          fill="currentColor"
          class="me-5 bi bi-person-x-fill text-danger link"
          viewBox="0 0 16 16"
        >
          <path
            fill-rule="evenodd"
            d="M1 14s-1 0-1-1 1-4 6-4 6 3 6 4-1 1-1 1H1zm5-6a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm6.146-2.854a.5.5 0 0 1 .708 0L14 6.293l1.146-1.147a.5.5 0 0 1 .708.708L14.707 7l1.147 1.146a.5.5 0 0 1-.708.708L14 7.707l-1.146 1.147a.5.5 0 0 1-.708-.708L13.293 7l-1.147-1.146a.5.5 0 0 1 0-.708z"
          />
        </svg>
      </div>
    </div>

    <div v-else class="text-center fs-2 fw-bold mt-5">
      <span
        class="spinner-border spinner-border"
        role="status"
        aria-hidden="true"
      ></span>
      Loading User Details
    </div>
  </div>
</template>

<script>
import { onMounted, ref } from "@vue/runtime-core";

import { useRouter } from "vue-router";
import axios from "axios";
export default {
  props: {
    id: String,
  },
  setup(props, { emit }) {
    const router = useRouter();
    var id = ref();
    var eachuser = ref();
    var show = ref(true);
    var edit = ref(false);
    var del = ref(true);

    function editfunc() {
      del.value = false;
      axios
        .put("https://testing-api-mock.herokuapp.com/users", eachuser.value)
        .then(() => {
          del.value = true;
          router.push("/users");
        })
        .catch(function (error) {
          del.value = true;
          console.log(error.message);
        });
    }

    function deluser() {
      del.value = false;
      axios
        .delete("https://testing-api-mock.herokuapp.com/users/" + id.value)
        .then(() => {
          del.value = true;
          router.push("/users");
        })
        .catch(function (error) {
          del.value = true;
          console.log(error.message);
        });
    }

    onMounted(() => {
      id.value = props.id;
      axios
        .get("https://testing-api-mock.herokuapp.com/users/" + id.value)
        .then((res) => {
          eachuser.value = res.data;
          console.log(eachuser.value);
        })
        .catch((err) => {
          console.log(err);
        });
    });

    return {
      eachuser,
      show,
      edit,
      editfunc,
      del,
      deluser,
    };
  },
};
</script>

<style>
</style>