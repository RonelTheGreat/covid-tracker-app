<template>
  <footer>
    <div class="logo">
      <img src="../assets/brand.svg" alt="brand" />
    </div>
    <p>rcob 2020</p>
  </footer>
</template>

<script>
export default {
  name: "AppFooter"
};
</script>

<style lang="scss" scoped>
footer {
  padding: 1%;
  display: flex;
  align-items: center;
  justify-content: space-between;

  p {
    color: #fff;
    font-size: 0.85rem;
  }
  .logo {
    img {
      max-width: 32px;
    }
  }
}
</style>