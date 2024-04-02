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

    this.$bus.$on("page-created", () => {
      this.pages = [...this.$pages.getAllPages()];
      // set a new array for the pages
    });

    this.$bus.$on("page-deleted", () => {
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

  mounted() {
    const savedPages = JSON.parse(localStorage.getItem("pages"));
    if (savedPages) {
      this.pages = savedPages;
    } else {
      this.pages = [
        {
          link: { text: "Home", url: "index.html" },
          pageTitle: "Home Page",
          content: "This is the home content",
          published: true,
        },
        {
          link: { text: "About", url: "about.html" },
          pageTitle: "About Page",
          content: "This is the about content",
          published: true,
        },
        {
          link: { text: "Contact", url: "contact.html" },
          pageTitle: "Contact Page",
          content: "This is the contact content",
          published: false,
        },
      ];
    }
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
