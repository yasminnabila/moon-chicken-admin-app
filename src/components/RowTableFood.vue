<script>
export default {
  name: "RowTableFood",
  data() {
    return {};
  },
  props: ["data", "index"],
  emits: ["readFoodById", "updateFoodStatus"],
  methods: {
    readFoodById(id) {
      this.$emit("readFoodById", id);
    },
    updateFoodStatus() {
      this.$emit("updateFoodStatus", this.data.status, this.data.id);
    },
  },
  computed: {
    infoUser() {
      return {
        email: localStorage.getItem("email"),
        role: localStorage.getItem("role"),
      };
    },
    rupiah() {
      return new Intl.NumberFormat("id-ID", {
        style: "currency",
        currency: "IDR",
        minimumFractionDigits: 0,
      }).format(this.data.price);
    },
  },
};
</script>

<template>
  <tr>
    <td class="fw-bold mb-1">{{ index + 1 }}</td>
    <td>{{ data.name }}</td>
    <td>{{ rupiah }}</td>
    <td>
      <div class="d-flex align-items-center">
        <img
          :src="data.imgUrl"
          alt=""
          style="width: 75px; height: 75px"
          class="rounded-circle"
        />
      </div>
    </td>
    <td>{{ data.Category.name }}</td>
    <td>{{ data.User.email }}</td>
    <td>
      <select
        class="form-select"
        aria-label="Default select example"
        v-model="data.status"
        @change="updateFoodStatus"
      >
        <option value="Active">Active</option>
        <option value="Inactive">Inactive</option>
        <option value="Archive">Archive</option>
      </select>
    </td>
    <td>
      <a
        v-if="infoUser.email === data.User.email || infoUser.role === 'Admin'"
        href="#"
        class="ms-3"
        @click="readFoodById(data.id)"
      >
        <i class="bi bi-pen" style="color: black"></i
      ></a>
    </td>
  </tr>
</template>

<style></style>
