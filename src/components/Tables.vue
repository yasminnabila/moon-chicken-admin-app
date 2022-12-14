<script>
import RowTableFood from "./RowTableFood.vue";
import RowTableCategories from "./RowTableCategories.vue";
import RowTableHistories from "./RowTableHistories.vue";
export default {
  name: "Tables",
  data() {
    return {};
  },
  props: ["foodData", "categoryData", "historyData", "whichPage"],
  emits: ["readFoodById", "updateFoodStatus"],
  methods: {
    readFoodById(id) {
      this.$emit("readFoodById", id);
    },
    updateFoodStatus(status, id) {
      this.$emit("updateFoodStatus", status, id);
    },
  },
  components: { RowTableFood, RowTableCategories, RowTableHistories },
};
</script>

<template>
  <!-- TABLE FOOD -->
  <table v-if="whichPage === 'foods'" class="table align-middle mb-0 bg-white">
    <thead class="bg-light">
      <tr>
        <th scope="col">#</th>
        <th scope="col">Name</th>
        <th scope="col">Price</th>
        <th scope="col">Image</th>
        <th scope="col">Category</th>
        <th scope="col">Author</th>
        <th scope="col">Status</th>
        <th scope="col"></th>
      </tr>
    </thead>
    <tbody>
      <RowTableFood
        v-for="(food, index) in foodData"
        :key="index"
        :data="food"
        :index="index"
        @readFoodById="readFoodById"
        @updateFoodStatus="updateFoodStatus"
      />
    </tbody>
  </table>
  <!-- TABLE FOOD END -->

  <!-- TABLE CATEGORIES -->
  <table
    v-else-if="whichPage === 'categories'"
    class="table align-middle mb-0 bg-white"
  >
    <thead class="bg-light">
      <tr>
        <th scope="col">#</th>
        <th scope="col">Name</th>
      </tr>
    </thead>
    <tbody>
      <RowTableCategories
        v-for="(data, index) in categoryData"
        :key="index"
        :data="data"
        :index="index"
      />
    </tbody>
  </table>
  <!-- TABLE CATEGORIES END -->

  <!-- TABLE HISTORY -->
  <table
    v-else-if="whichPage === 'histories'"
    class="table align-middle mb-0 bg-white"
  >
    <thead class="bg-light">
      <tr>
        <th scope="col">#</th>
        <th scope="col">Product Name</th>
        <th scope="col">Description</th>
        <th scope="col">Created At</th>
        <th scope="col">Updated By</th>
      </tr>
    </thead>
    <tbody>
      <RowTableHistories
        v-for="(data, index) in historyData"
        :key="index"
        :data="data"
        :index="index"
      />
    </tbody>
  </table>
  <!-- TABLE HISTORY END -->
</template>
