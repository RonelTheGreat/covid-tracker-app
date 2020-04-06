<template>
  <div class="load">
    <div class="line"></div>
    <div class="line"></div>
    <div class="line"></div>
  </div>
</template>

<script>
export default {
  name: "AppLoading"
};
</script>

<style lang="scss" scoped>
$primary-color: #37d851;
$secondary-color: #570f83;

.load {
  margin: 50vh auto;
  text-align: center;
}
.load .line:nth-last-child(1) {
  animation: loadingC 0.6s 0.1s linear infinite;
}
.load .line:nth-last-child(2) {
  animation: loadingC 0.6s 0.2s linear infinite;
}
.load .line:nth-last-child(3) {
  animation: loadingC 0.6s 0.3s linear infinite;
}

.line {
  display: inline-block;
  width: 15px;
  height: 15px;
  border-radius: 15px;
  background-color: $primary-color;
  margin-left: 0.3rem;
}

@keyframes loadingC {
  0% {
    transform: translate(0, 0);
  }
  50% {
    transform: translate(0, 15px);
  }
  100% {
    transform: translate(0, 0);
  }
}
</style>