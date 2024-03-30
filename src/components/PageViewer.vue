<template>
  <div class="container">
    <h1>Page Title</h1>
    <p>content</p>
  </div>
</template>

<script>
export default {
  created() {
    console.log(this.$route.params);
  },
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
