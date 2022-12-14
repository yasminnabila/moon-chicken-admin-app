<script>
import FormFood from "../components/FormFood.vue";
export default {
  name: "AddFoodPage",
  data() {
    return {};
  },
  props: ["categoryData", "foodData", "whichPage", "foodDataById"],
  emits: ["cancelFormFood", "addFood"],
  methods: {
    cancelFormFood() {
      this.$emit("cancelFormFood");
    },
    addFood(data) {
      this.$emit("addFood", data);
    },
  },
  components: { FormFood },
};
</script>

<template>
  <section class="vh-100" style="background-color: #d1c4e9; min-height: 100vh">
    <div
      class="container py-12 h-50 justify-content-center align-items-center"
      style="transform: scale(75%)"
    >
      <div class="row d-flex justify-content-center align-items-center h-50">
        <div class="col-lg-12 col-xl-7">
          <div class="card rounded-3">
            <img
              src="../assets/newfood.jpeg"
              class="w-100"
              style="
                border-top-left-radius: 0.3rem;
                border-top-right-radius: 0.3rem;
              "
              alt="Sample photo"
            />
            <div class="card-body p-4 p-md-5">
              <h3 class="mb-4 pb-2 pb-md-0 mb-md-5 px-md-2">
                Add New Moon Chicken Menu
              </h3>
              <FormFood
                :foodData="foodData"
                :categoryData="categoryData"
                :whichPage="whichPage"
                :foodDataById="foodDataById"
                @cancelFormFood="cancelFormFood"
                @addFood="addFood"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
