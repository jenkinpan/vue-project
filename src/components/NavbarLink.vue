<template>
  <li>
    <router-link
      :to="`/${index}`"
      class="nav-link"
      active-class="text-decoration-underline active"
      aria-current="page"
      :title="`This goes to the ${page.link.text} page`"
      >{{ page.link.text }}</router-link
    >
  </li>
</template>

<script>
export default {
  props: ["page", "index"],
};
</script>
