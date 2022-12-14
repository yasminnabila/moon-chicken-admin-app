<script>
import axios from "axios";
import NavBar from "./views/NavBar.vue";
import RegisterPage from "./views/RegisterPage.vue";
import LoginPage from "./views/LoginPage.vue";
import DashboardPage from "./views/DashboardPage.vue";
import FoodPage from "./views/FoodPage.vue";
import CategoriesPage from "./views/CategoriesPage.vue";
import HistoriesPage from "./views/HistoriesPage.vue";
import AddFoodPage from "./views/AddFoodPage.vue";
import EditFoodPage from "./views/EditFoodPage.vue";
import AddCategoryPage from "./views/AddCategoryPage.vue";
import Loader from "./components/Loader.vue";
let baseUrl = `https://moon-chicken.herokuapp.com/`;

export default {
  name: "App",
  data() {
    return {
      isLoading: false,
      whichPage: "",
      foodData: [],
      categoryData: [],
      historyData: [],
      foodDataById: [],
      googleLogin: "buttonDiv",
    };
  },
  components: {
    NavBar,
    RegisterPage,
    LoginPage,
    DashboardPage,
    FoodPage,
    CategoriesPage,
    HistoriesPage,
    AddFoodPage,
    EditFoodPage,
    AddCategoryPage,
    Loader,
  },
  methods: {
    changePage(page) {
      this.whichPage = page;
    },
    async dashboard() {
      try {
        await this.readFood();
        await this.readCategories();
        await this.readHistories();
        this.changePage(`dashboard`);
      } catch (error) {
        console.log(error);
      }
    },
    //? ALL SESSIONS
    //? SIGN UP
    async submitRegister(childObj) {
      try {
        const { username, email, password, phoneNumber, address } = childObj;
        await axios({
          method: `POST`,
          url: baseUrl + `register`,
          data: {
            username,
            email,
            password,
            phoneNumber,
            address,
          },
        });
        this.changePage("login");
        Swal.fire({
          icon: "success",
          title: `Yeay, you are now registered!`,
          text: "Now you may sign in to use our services",
          confirmButtonText: "Sign in now",
        });
      } catch (error) {
        Swal.fire({
          icon: "error",
          title: "Oops! Something happened...",
          text: error.response.data.message,
          confirmButtonText: "Try Again",
        });
      }
    },
    //? SIGN IN
    async submitLogin(childObj) {
      try {
        const { email, password } = childObj;
        const dataLogin = await axios({
          method: "POST",
          url: baseUrl + `login`,
          data: {
            email,
            password,
          },
        });
        localStorage.setItem("access_token", dataLogin.data.access_token);
        localStorage.setItem("email", dataLogin.data.email);
        localStorage.setItem("username", dataLogin.data.username);
        localStorage.setItem("id", dataLogin.data.id);
        localStorage.setItem("role", dataLogin.data.role);
        this.dashboard();
        Swal.fire({
          icon: "success",
          title: "Success signing in!",
          text: `Welcome to Moon Chicken, ${dataLogin.data.username}!`,
          showConfirmButton: false,
          timer: 1500,
        });
      } catch (error) {
        Swal.fire({
          icon: "error",
          title: "Oops! Something happened...",
          text: error.response.data.message,
          confirmButtonText: "Try Again",
        });
      }
    },
    //? LOGOUT
    async handleLogOut() {
      Swal.fire({
        title: "Are you sure?",
        text: "You will be missed!",
        icon: "warning",
        showCancelButton: true,
        confirmButtonColor: "#3085d6",
        cancelButtonColor: "#d33",
        confirmButtonText: "Signing out!",
      }).then((result) => {
        if (result.isConfirmed) {
          Swal.fire({
            position: "top-end",
            icon: "success",
            title: "Signed out",
            text: "See you later, Moonlander!",
            showConfirmButton: false,
            timer: 1500,
          });
          localStorage.clear();
          this.changePage("login");
        }
      });
    },
    //? GOOGLE LOG IN
    async handleCredentialResponse(response) {
      try {
        let data = await axios({
          url: baseUrl + `google-sign-in`,
          method: "POST",
          headers: {
            access_token_google: response.credential,
          },
        });
        localStorage.setItem("access_token", data.data.access_token);
        localStorage.setItem("email", data.data.email);
        localStorage.setItem("username", data.data.username);
        localStorage.setItem("id", data.data.id);
        localStorage.setItem("role", data.data.role);
        this.dashboard();
        Swal.fire({
          icon: "success",
          title: "Success signing in!",
          text: `Welcome to Moon Chicken!`,
          showConfirmButton: false,
          timer: 1500,
        });
      } catch (error) {
        Swal.fire({
          icon: "error",
          title: "Oops! Something happened...",
          text: "Try login with other method",
          confirmButtonText: "Try Again",
        });
      }
    },
    //? FOOD
    //? READ FOOD
    async readFood() {
      try {
        this.isLoading = true;
        const dataFood = await axios({
          url: baseUrl + `food`,
          method: "GET",
          headers: {
            access_token: localStorage.getItem("access_token"),
          },
        });
        this.foodData = dataFood.data.data;
      } catch (error) {
        console.log(error.response.data.message);
      } finally {
        this.isLoading = false;
      }
    },
    //? FETCH FOOD DATA
    async readFoodById(id) {
      try {
        this.isLoading = true;
        let dataFoodById = await axios({
          url: baseUrl + `food/` + id,
          method: "GET",
          headers: {
            access_token: localStorage.getItem("access_token"),
          },
        });
        this.foodDataById = dataFoodById.data.data;
        this.changePage("editfood");
      } catch (error) {
        console.log(error.response.data.message);
      } finally {
        this.isLoading = false;
      }
    },
    // ? EDIT FOOD
    async editFood(obj, id) {
      try {
        let data = await axios({
          url: baseUrl + `food/` + id,
          method: "PUT",
          headers: {
            access_token: localStorage.getItem("access_token"),
          },
          data: obj,
        });
        Swal.fire("Yeay!", "Success editing menu", "success");
        await this.readFood();
        await this.readHistories();
        this.whichPage = "foods";
      } catch (error) {
        Swal.fire({
          icon: "error",
          title: "Oops! Failed to edit menu menu...",
          text: error.response.data.message,
          confirmButtonText: "Try Again",
        });
      }
    },
    //delete
    // async deleteCategories(id, page) {
    //   try {
    //     await axios({
    //       url: `${baseUrl}/categories/${id}`,
    //       method: "DELETE",
    //       headers: {
    //         access_token: localStorage.getItem("access_token"),
    //       },
    //     });
    //     this.showCategories();
    //     this.changePage(page);
    //     Swal.fire(
    //       'Category deleted!',
    //       'The category has been deleted',
    //       'success'
    //     )
    //   } catch (error) {
    //     Swal.fire({
    //       icon: "error",
    //       title: "Oops...",
    //       text: `${error.response.data.msg}`,
    //     });
    //   }
    // },
    //? ADD FOOD
    async addFood(obj) {
      try {
        await axios({
          url: baseUrl + `food`,
          method: "POST",
          headers: {
            access_token: localStorage.getItem("access_token"),
          },
          data: obj,
        });
        Swal.fire("Yeay!", "Success adding new menu", "success");
        await this.readFood();
        await this.readHistories();
        this.whichPage = "foods";
      } catch (error) {
        Swal.fire({
          icon: "error",
          title: "Oops! Failed to add new menu...",
          text: error.response.data.message,
          confirmButtonText: "Try Again",
        });
      }
    },
    //? STATUS FOOD
    async updateFoodStatus(status, id) {
      try {
        let data = await axios({
          url: baseUrl + `food/` + id,
          method: "PATCH",
          headers: {
            access_token: localStorage.getItem("access_token"),
          },
          data: {
            status: status,
          },
        });
        Swal.fire("Yeay!", "Status has been updated", "success");
        await this.readFood();
        await this.readHistories();
      } catch (error) {
        Swal.fire({
          icon: "error",
          title: "Oops! Failed to update food stataus",
          text: error.response.data.message,
          confirmButtonText: "Try Again",
        });
      } finally {
        this.readFood();
      }
    },
    //? CATEGORIES
    async readCategories() {
      try {
        this.isLoading = true;
        const dataCategories = await axios({
          url: baseUrl + `categories`,
          method: "GET",
          headers: {
            access_token: localStorage.getItem("access_token"),
          },
        });
        this.categoryData = dataCategories.data.data;
      } catch (error) {
        console.log(error.response.data.message);
      } finally {
        this.isLoading = false;
      }
    },
    //? ADD FOOD
    async addCategory(obj) {
      try {
        await axios({
          url: baseUrl + `categories`,
          method: "POST",
          headers: {
            access_token: localStorage.getItem("access_token"),
          },
          data: obj,
        });
        Swal.fire("Yeay!", "Success adding new category", "success");
        await this.readCategories();
        await this.readHistories();
      } catch (error) {
        Swal.fire({
          icon: "error",
          title: "Oops! Failed to add new category...",
          text: error.response.data.message,
          confirmButtonText: "Try Again",
        });
      } finally {
        this.changePage("categories");
      }
    },
    //? HISTORIES
    async readHistories() {
      try {
        this.isLoading = true;
        const dataHistories = await axios({
          url: baseUrl + `histories`,
          method: "GET",
          headers: {
            access_token: localStorage.getItem("access_token"),
          },
        });
        this.historyData = dataHistories.data.data;
      } catch (error) {
        console.log(error.response.data.message);
      } finally {
        this.isLoading = false;
      }
    },
  },
  async created() {
    if (localStorage.getItem(`access_token`)) {
      await this.readFood();
      await this.readCategories();
      await this.readHistories();
      this.changePage(`dashboard`);
    } else {
      this.changePage(`login`);
    }
  },
  mounted() {
    let cb = this.handleCredentialResponse;
    window.onload = function () {
      google.accounts.id.initialize({
        client_id:
          "223085130115-r5sr8hjasmkm7irtngg5i0hmunh3ilu1.apps.googleusercontent.com",
        callback: cb,
      });
      google.accounts.id.renderButton(document.getElementById("buttonDiv"), {
        theme: "outline",
        size: "large",
      });
      google.accounts.id.prompt();
    };
    window.onclick = function () {
      google.accounts.id.initialize({
        client_id:
          "223085130115-r5sr8hjasmkm7irtngg5i0hmunh3ilu1.apps.googleusercontent.com",
        callback: cb,
      });
      google.accounts.id.renderButton(document.getElementById("buttonDiv"), {
        theme: "outline",
        size: "large",
      });
      google.accounts.id.prompt();
    };
  },
};
</script>

<template>
  <!-- NAVBAR SECTION -->
  <NavBar
    v-if="whichPage !== 'login' && whichPage !== 'register'"
    @dashboard="changePage('dashboard')"
    @foods="changePage('foods')"
    @categories="changePage('categories')"
    @histories="changePage('histories')"
    @logout="handleLogOut"
  />
  <!-- NAVBAR SECTION END -->

  <!-- LOADER SECTION -->
  <Loader v-show="isLoading" />
  <div v-show="!isLoading">
    <!-- LOG IN SECTION -->
    <LoginPage
      v-if="whichPage === 'login'"
      :googleLogin="googleLogin"
      @register="changePage('register')"
      @submitLogin="submitLogin"
    />
    <!-- LOG IN SECTION END -->

    <!-- SIGN UP SECTION -->
    <RegisterPage
      v-else-if="whichPage === 'register'"
      @submitRegister="submitRegister"
      @login="changePage('login')"
    />
    <!-- SIGN UP SECTION END -->

    <!-- DASHBOARD SECTION -->
    <DashboardPage
      v-else-if="whichPage === 'dashboard'"
      :totalFood="foodData.length"
      :totalCategory="categoryData.length"
    />
    <!-- DASHBOARD SECTION END -->

    <!-- TABLE FOOD SECTION -->
    <FoodPage
      v-else-if="whichPage === 'foods'"
      :foodData="foodData"
      :whichPage="whichPage"
      @addFoodPage="changePage('addfood')"
      @readFoodById="readFoodById"
      @updateFoodStatus="updateFoodStatus"
    />
    <!-- TABLE FOOD SECTION END -->

    <!-- TABLE CATEGORIES SECTION -->
    <CategoriesPage
      v-else-if="whichPage === 'categories'"
      :categoryData="categoryData"
      :whichPage="whichPage"
      @addCategoryPage="changePage('addcategory')"
    />
    <!-- TABLE CATEGORIES SECTION END -->

    <!-- TABLE HISTORIES SECTION -->
    <HistoriesPage
      v-else-if="whichPage === 'histories'"
      :historyData="historyData"
      :whichPage="whichPage"
    />
    <!-- TABLE HISTORIES SECTION END -->

    <!-- NEW FOOD FORM SECTION -->
    <AddFoodPage
      v-else-if="whichPage === 'addfood'"
      :foodData="foodData"
      :categoryData="categoryData"
      :whichPage="whichPage"
      @cancelFormFood="changePage('foods')"
      @addFood="addFood"
    />
    <!-- NEW FOOD FORM SECTION END -->

    <!-- EDIT FOOD SECTION -->
    <EditFoodPage
      v-else-if="whichPage === 'editfood'"
      :foodDataById="foodDataById"
      :categoryData="categoryData"
      :whichPage="whichPage"
      @cancelFormFood="changePage('foods')"
      @editFood="editFood"
      @readFoodById="readFoodById"
    />
    <!-- EDIT FOOD SECTION END -->

    <!-- NEW CATEGORY FORM SECTION -->
    <AddCategoryPage
      v-else-if="whichPage === 'addcategory'"
      :categoryData="categoryData"
      :whichPage="whichPage"
      @cancelFormCategories="changePage('categories')"
      @addCategory="addCategory"
    />
    <!-- NEW CATEGORY FORM SECTION END -->
  </div>
  <!-- LOADER END -->
</template>

<style></style>
