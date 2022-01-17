<template>
  <header class="header">
    <div class="container">
      <img src="../assets/img/logo.svg" alt="Logo" class="logo" />
    </div>
  </header>
</template>

<script>
export default {
  name: 'Header',
};
</script>

<style lang='scss' scoped>
@import '../assets/scss/partials/_variables.scss';
.header {
  background-color: $headerBgColor;
  .container {
    display: flex;
    align-items: center;
    height: 80px;
    padding-left: 1rem;
      .logo {
        height: 50px;
        border-radius: 50%;
        background-color: black;
      }
  }
}
</style>
