<template>
  <div class="container">
    <h1>{{ page.pageTitle }}</h1>
    <p>{{ page.content }}</p>
  </div>
</template>

<script>
export default {
  props: ["page"],
};
</script>

<style scoped>
h1 {
  color: #240a34;
}
p {
  color: #891652;
}
</style>
