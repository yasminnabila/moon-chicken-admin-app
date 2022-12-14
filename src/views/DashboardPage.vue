<script>
export default {
  name: "DashboardPage",
  data() {
    return {};
  },
  props: ["totalFood", "totalCategory"],
};
</script>

<template>
  <section
    id="dashboard-section"
    style="
      background: linear-gradient(to bottom, #ddd6f3 0%, #faaca8 99%);
      height: 100vh;
    "
  >
    <div
      class="container align-items-center justify-content-center;"
      style="transform: scale(95%)"
    >
      <br />
      <!-- TITLE: DASHBOARD -->
      <h1
        class="display-2 text-center align-items-center justify-content-center;"
      >
        Dashboard
      </h1>
      <div
        id="cards"
        class="container align-items-center justify-content-center;"
      >
        <br />
        <!-- ROW FOR CARD -->
        <div class="row d-flex justify-content-center">
          <div class="col-12 col-md-6">
            <div class="row">
              <!-- TOTAL MENU CARD -->
              <div class="col-12 col-md-6 mb-3;">
                <div class="card">
                  <div class="card-body">
                    <div
                      style="
                        display: flex;
                        justify-content: space-between;
                        align-items: center;
                        margin-top: 0.5rem;
                      "
                    >
                      <h6
                        class="card-subtitle mb-2 text-muted"
                        style="font-size: 1.5rem"
                      >
                        Total Food
                      </h6>
                      <i class="bi bi-box2-heart" style="font-size: 2rem"></i>
                    </div>
                    <h6
                      class="card-title card-number"
                      id="total-food"
                      style="font-size: 1.5rem"
                    >
                      {{ totalFood }}
                    </h6>
                  </div>
                </div>
              </div>

              <!-- TOTAL CATEGORIES CARD -->
              <div class="col-12 col-md-6 mb-3">
                <div class="card">
                  <div class="card-body">
                    <div
                      style="
                        display: flex;
                        justify-content: space-between;
                        align-items: center;
                        margin-top: 0.5rem;
                      "
                    >
                      <h6
                        class="card-subtitle mb-2 text-muted"
                        style="font-size: 1.5rem"
                      >
                        Total Categories
                      </h6>
                      <i class="bi bi-journals" style="font-size: 2rem"></i>
                    </div>
                    <h6
                      class="card-title card-number"
                      id="total-category"
                      style="font-size: 1.5rem"
                    >
                      {{ totalCategory }}
                    </h6>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style>
#cards {
  margin-top: 1rem;
}
</style>
