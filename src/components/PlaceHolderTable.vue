<template>
  <div>
    <table class="table table-success border-none">
      <thead>
        <tr>
          <td colspan="3">
            <input
              type="text"
              class="rounded p-1 border-info"
              placeholder="Search Name,Email and Positions"
            />
          </td>
          <td><button class="btn btn-primary btn-sm w-100">Add</button></td>
        </tr>
        <tr>
          <th scope="col">Name</th>
          <th scope="col">Email</th>
          <th scope="col">Phone</th>
          <th scope="col">Position</th>
        </tr>
      </thead>
      <tbody>
        <tr style="height: 120px" class="p-4">
          <td colspan="4" class="text-center">
            <div class=" mt-5 spinner-border" role="status">
  <span class="visually-hidden">Loading...</span>
</div>
          </td>
        </tr>
        <tr>
          <td colspan="2" class="fw-bold placeholder-glow">
            Page <span class="placeholder col-1 rounded-pill"></span> of
            <span class="placeholder col-1 rounded-pill"></span>
          </td>
          <td colspan="2" class="text-end me-3">
            <span>
              <svg
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
            <span class="mx-3"
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
      </tbody>
    </table>
  </div>
</template>

<script>
export default {};
</script>

<style>
</style>