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
    height: 80px;
    align-items: center;
    padding-left: 1rem;
      .logo {
        height: 50px;
        background-color: black;
        border-radius: 50%;
      }
  }
}
</style>
