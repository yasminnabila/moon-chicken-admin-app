<script>
import Buttons from "./Buttons.vue";
export default {
  name: "FormFood",
  data() {
    return {
      name: "",
      description: "",
      price: "",
      image: "",
      category: "",
    };
  },
  props: ["categoryData", "whichPage", "foodDataById"],
  emits: ["cancelFormFood", "addFood", "editFood"],
  methods: {
    cancelFormFood() {
      this.$emit("cancelFormFood");
    },
    handleSubmit() {
      if (this.whichPage === "addfood") {
        this.$emit("addFood", {
          name: this.name,
          description: this.description,
          price: this.price,
          imgUrl: this.image,
          categoryId: this.category,
        });
      } else if (this.whichPage === "editfood") {
        this.$emit("editFood", {
          name: this.name,
          description: this.description,
          price: this.price,
          imgUrl: this.image,
          categoryId: this.category,
        });
      }
    },
  },
  created() {
    if (this.whichPage === "editfood") {
      this.name = this.foodDataById.name;
      this.description = this.foodDataById.description;
      this.price = this.foodDataById.price;
      this.image = this.foodDataById.imgUrl;
      this.category = this.foodDataById.categoryId;
    }
  },
  components: { Buttons },
};
</script>

<template>
  <!-- New Food Form -->
  <form id="food-form" @submit.prevent="handleSubmit">
    <!-- Name of Food -->
    <div class="mb-3">
      <label for="edit-food-name"
        >Name <span class="text-danger fw-bold">*</span></label
      >
      <input
        type="text"
        class="form-control"
        id="edit-food-name"
        v-model="name"
        placeholder="Enter food name"
        autocomplete="off"
        required
      />
    </div>
    <!-- Name End -->

    <!-- Category -->
    <div class="mb-3">
      <label for="edit-food-category"
        >Category <span class="text-danger fw-bold">*</span></label
      >
      <br />
      <select
        v-model="category"
        id="edit-food-category"
        class="form-select"
        aria-label="Default select example"
      >
        <option selected disabled>-- Select Category --</option>
        <option
          v-for="category in categoryData"
          :key="category.id"
          :value="category.id"
        >
          {{ category.name }}
        </option>
      </select>
    </div>
    <!-- Category End -->

    <!-- Description -->
    <div class="mb-3">
      <label for="edit-food-desc"
        >Description <span class="text-danger fw-bold">*</span></label
      >
      <input
        type="text"
        class="form-control"
        id="edit-food-desc"
        v-model="description"
        placeholder="Enter food description"
        autocomplete="off"
        required
      />
    </div>
    <!-- Description End -->

    <div class="row">
      <!-- Food Price -->
      <div class="col-12 col-md-6">
        <div class="mb-3">
          <label for="edit-food-price"
            >Price <span class="text-danger fw-bold">*</span></label
          >
          <input
            type="number"
            min="0"
            class="form-control"
            id="edit-food-price"
            v-model="price"
            placeholder="Enter food price"
            autocomplete="off"
            required
          />
        </div>
      </div>
    </div>
    <!-- Food Price End -->

    <!-- Food Image -->
    <div class="mb-3">
      <label for="edit-food-image"
        >Image <span class="text-danger fw-bold">*</span></label
      >
      <input
        type="url"
        class="form-control"
        id="edit-food-image"
        v-model="image"
        placeholder="Enter food image url"
        autocomplete="off"
        required
      />
    </div>
    <!-- Food Image End -->

    <!-- Cancel Button -->
    <div class="row mt-5 mb-3">
      <!-- Cancel Button -->
      <div class="col-6">
        <Buttons
          @click="cancelFormFood"
          :class="'btn btn-md btn-primary rounded-pill w-100 p-2 mt-3'"
          :style="'background-color: #6a1b9a'"
          :type="'button'"
          :title="'Cancel'"
        />
      </div>
      <!-- Cancel Button End -->

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
  <!-- New Food Form End -->
</template>
