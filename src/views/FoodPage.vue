<script>
import Tables from "../components/Tables.vue";

export default {
  name: "FoodPage",
  data() {
    return {};
  },
  props: ["foodData", "whichPage"],
  emits: ["addFoodPage", "readFoodById", "updateFoodStatus"],
  methods: {
    addFoodPage() {
      this.$emit("addFoodPage");
    },
    readFoodById(id) {
      this.$emit("readFoodById", id);
    },
    updateFoodStatus(status, id) {
      this.$emit("updateFoodStatus", status, id);
    },
  },
  components: { Tables },
};
</script>

<template>
  <section
    id="food-section"
    style="
      background: linear-gradient(to bottom, #ddd6f3 0%, #faaca8 99%)
      width: auto;
      min-height: 100vh;
    "
  >
    <div class="container align-items-center justify-content-center">
      <br />
      <!-- TITLE AND BUTTON -->
      <div
        style="
          display: flex;
          justify-content: space-between;
          align-items: center;
          transform: scale(85%);
        "
      >
        <div>
          <h3 class="display-3">Menu</h3>
        </div>
        <div>
          <!-- Button New Food -->
          <button class="btn btn-dark" id="new-food" @click="addFoodPage">
            <span class="icon material-symbols-outlined"></span>Add New Food
          </button>
          <!-- Button New Food End -->
        </div>
      </div>
      <!-- TITLE AND BUTTON END -->
    </div>

    <div class="container my-6" style="transform: scale(85%)">
      <div class="shadow-4 rounded-5 overflow-hidden">
        <Tables
          :foodData="foodData"
          :whichPage="whichPage"
          @readFoodById="readFoodById"
          @updateFoodStatus="updateFoodStatus"
        />
      </div>
    </div>
  </section>
</template>
