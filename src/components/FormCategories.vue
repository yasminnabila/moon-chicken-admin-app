<script>
import Buttons from "./Buttons.vue";
export default {
  name: "FormCategories",
  data() {
    return {
      name: "",
    };
  },
  props: ["categoryData", "whichPage"],
  emits: ["cancelFormCategories", "addCategory"],
  methods: {
    cancelFormCategories() {
      this.$emit("cancelFormCategories");
    },
    addCategory() {
      this.$emit("addCategory", {
        name: this.name,
      });
    },
  },
  components: { Buttons },
};
</script>

<template>
  <!-- New Category Form -->
  <form id="category-form" @submit.prevent="addCategory">
    <!-- Name -->
    <div class="mb-3">
      <label for="category-name"
        >Name <span class="text-danger fw-bold">*</span></label
      >
      <input
        type="text"
        class="form-control"
        id="category-name"
        v-model="name"
        placeholder="Enter category name"
        autocomplete="off"
        required
      />
    </div>
    <!-- Name End -->

    <!-- Cancel Button -->
    <div class="row mt-5 mb-3">
      <div class="col-6">
        <Buttons
          :class="'btn btn-md btn-primary rounded-pill w-100 p-2 mt-3'"
          :style="'background-color: #6a1b9a'"
          :type="'button'"
          :title="'Cancel'"
          @click.prevent="cancelFormCategories"
        />
      </div>
      <!-- End Cancel Button -->

      <!-- Submit Button -->
      <div class="col-6">
        <Buttons
          :class="'btn btn-md btn-primary rounded-pill w-100 p-2 mt-3'"
          :style="'background-color: #6a1b9a'"
          :type="'submit'"
          :title="'Submit'"
        />
      </div>
      <!-- Submit Button End -->
    </div>
  </form>
  <!-- New Category Form End -->
</template>
