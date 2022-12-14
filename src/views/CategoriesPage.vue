<script>
import Tables from "../components/Tables.vue";
export default {
  name: "CategoriesPage",
  data() {
    return {};
  },
  props: ["categoryData", "whichPage"],
  emits: ["addCategoryPage"],
  methods: {
    addCategoryPage() {
      this.$emit("addCategoryPage");
    },
  },
  components: { Tables },
};
</script>

<template>
  <section
    id="categories-section"
    style="
      background: linear-gradient(to bottom, #ddd6f3 0%, #faaca8 99%);
      min-height: 100vh;
    "
  >
    <div class="container align-items-center justify-content-center">
      <div
        style="
          display: flex;
          justify-content: space-between;
          align-items: center;
          transform: scale(85%);
        "
      >
        <div>
          <br />
          <h3 class="display-3">Categories</h3>
        </div>
        <div>
          <!-- Button New Category -->
          <button
            class="btn btn-dark"
            id="new-category"
            @click.prevent="addCategoryPage"
          >
            <span class="icon material-symbols-outlined"></span>Add New Category
          </button>
          <!-- Button New Category End -->
        </div>
      </div>
    </div>
    <div class="container my-6" style="transform: scale(85%)">
      <div class="shadow-4 rounded-5 overflow-hidden">
        <Tables :categoryData="categoryData" :whichPage="whichPage" />
      </div>
    </div>
  </section>
</template>
