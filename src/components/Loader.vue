<template>
<div>
    <h3>Caricamento in corso ...</h3>
</div>
</template>

<script>
export default {
  name: 'Loader',
};
</script>

<style lang="scss" scoped>
div {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    font-size: 2rem;
    height: calc(100vh - 80px - 5rem * 2);
    background-color: red;
    color:white;
    h2 {
        font-size: 2rem;
    }
}
</style>
