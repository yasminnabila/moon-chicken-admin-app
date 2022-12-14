<script>
import FormCategories from "../components/FormCategories.vue";
export default {
  name: "AddCategoryPage",
  data() {
    return {};
  },
  props: ["categoryData", "whichPage"],
  emits: ["cancelFormCategories", "addCategory"],
  methods: {
    cancelFormCategories() {
      this.$emit("cancelFormCategories");
    },
    addCategory(data) {
      this.$emit("addCategory", data);
    },
  },
  components: { FormCategories },
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
              src="../assets/newcategory.jpeg"
              class="w-100"
              style="
                border-top-left-radius: 0.3rem;
                border-top-right-radius: 0.3rem;
              "
              alt="Sample photo"
            />
            <div class="card-body p-4 p-md-5">
              <h3 class="mb-4 pb-2 pb-md-0 mb-md-5 px-md-2">
                Add New Category
              </h3>
              <FormCategories
                :categoryData="categoryData"
                :whichPage="whichPage"
                @cancelFormCategories="cancelFormCategories"
                @addCategory="addCategory"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
