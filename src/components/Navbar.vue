<template>
  <nav
    :class="[`navbar-${theme}`, `bg-${theme}`, 'navbar', 'navbar-expand-lg']"
  >
    <div class="container-fluid">
      <a href="#" class="navbar-brand">My Vue</a>
      <ul class="mb-2 navbar-nav me-auto mb-lg-0">
        <navbar-link
          v-for="(page, index) in publishedPages"
          class="nav-item"
          :key="index"
          :page="page"
          :index="index"
        >
        </navbar-link>
        <li>
          <router-link
            to="/pages"
            class="nav-link"
            active-class="text-decoration-underline active"
            aria-current="page"
            >Pages</router-link
          >
        </li>
      </ul>
      <form class="d-flex">
        <button class="btn btn-primary" @click.prevent="changeTheme()">
          Toggle Navbar
        </button>
      </form>
    </div>
  </nav>
</template>

<script>
import NavbarLink from "./NavbarLink.vue";
export default {
  components: {
    NavbarLink,
  },

  inject: ["$pages", "$bus"],

  created() {
    this.getThemeSetting();

    this.pages = this.$pages.getAllPages();

    this.$bus.$on("page-updated", () => {
      this.pages = [...this.$pages.getAllPages()];
      // set a new array for the pages
    });
  },

  computed: {
    publishedPages() {
      return this.pages.filter((p) => p.published);
    },
  },

  data() {
    return {
      theme: "light",
      pages: [],
    };
  },

  methods: {
    changeTheme() {
      let theme = "light";
      if (this.theme == "light") {
        theme = "dark";
      }
      this.theme = theme;
      this.storeThemeSetting();
    },
    storeThemeSetting() {
      localStorage.setItem("theme", this.theme);
    },
    getThemeSetting() {
      let theme = localStorage.getItem("theme");

      if (theme) {
        this.theme = theme;
      }
    },
  },
};
</script>
