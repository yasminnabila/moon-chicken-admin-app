<script>
import Tables from "../components/Tables.vue";
export default {
  name: "HistoriesPage",
  data() {
    return {};
  },
  props: ["historyData", "whichPage"],
  components: { Tables },
};
</script>

<template>
  <section
    id="logs-section"
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
          <h3 class="display-3">Logs</h3>
        </div>
      </div>
    </div>
    <div class="container my-6" style="transform: scale(85%)">
      <div class="shadow-4 rounded-5 overflow-hidden">
        <Tables :historyData="historyData" :whichPage="whichPage" />
      </div>
    </div>
  </section>
</template>
