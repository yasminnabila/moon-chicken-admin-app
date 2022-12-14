<script>
export default {
  name: "NavBar",
  data() {
    return {
      username: "",
    };
  },
  // props: ["changePage"],
  emits: ["dashboard", "foods", "categories", "histories", "logout"],
  methods: {
    dashboard() {
      this.$emit("dashboard");
    },
    foods() {
      this.$emit("foods");
    },
    categories() {
      this.$emit("categories");
    },
    histories() {
      this.$emit("histories");
    },
    logout() {
      this.$emit("logout");
    },
  },
  computed: {
    infoUser() {
      return {
        username: localStorage.getItem("username"),
      };
    },
  },
};
</script>

<template>
  <section class="navbar-section" id="navbar-section">
    <nav
      class="navbar sticky-top navbar-expand-lg navbar-light bg-light"
      id="navbar-menu"
    >
      <div class="container-fluid" style="height: 25px">
        <div>
          <!-- COMPANY LOGO -->
          <a class="navbar-brand flex me-30" href="#" @click.prevent="">
            <img
              src="../assets/logonew.png"
              alt="logo"
              width="35"
              class="m-auto"
            />
          </a>
          <!-- COMPANY NAME -->
          <a class="navbar-brand" href="#">Moon Chicken</a>
        </div>
        <button
          class="navbar-toggler position-absolute d-md-none collapsed"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#sidebar-menu"
          aria-controls="sidebar-menu"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbar-login">
          <div class="navbar">
            <ul class="navbar-nav mr-auto">
              <!-- BUTTON DASHBOARD -->
              <li class="nav-item active">
                <a
                  @click.prevent="dashboard"
                  class="nav-link"
                  aria-current="page"
                  href="#"
                >
                  Dashboard
                </a>
              </li>

              <!-- BUTTON MENU -->
              <li class="nav-item active">
                <a @click.prevent="foods" class="nav-link" href="#"> Menu </a>
              </li>

              <!-- BUTTON CATEGORIES -->
              <li class="nav-item active">
                <a @click.prevent="categories" class="nav-link" href="#">
                  Categories
                </a>
              </li>

              <!-- BUTTON HISTORY -->
              <li class="nav-item active">
                <a @click.prevent="histories" class="nav-link" href="#">
                  Logs
                </a>
              </li>
            </ul>
          </div>
        </div>

        <!-- BUTTON LOGOUT -->
        <div>
          <ul class="navbar-nav mr-auto">
            <li class="nav-item">
              <a class="nav-link text-dark">
                <span class="icon material-symbols-outlined me-2"></span
                >Annyeong,
                <span id="nav-username">{{ infoUser.username }}!</span></a
              >
            </li>
            <li class="nav-item active">
              <div>
                <a @click.prevent="logout" class="nav-link" href="#">
                  Logout
                </a>
              </div>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </section>
</template>
