<template>
  <div class="Timeout">
    <div class="progressBar"></div>
  </div>
</template>

<script>
export default {
  mounted() {
    // setInterval(() => {
    //   console.log("Next meme");
    // }, 5000);
  },
};
</script>

<style lang="scss">
.Timeout {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 5px;
  background: rgba(0, 0, 0, 0.164);
  backdrop-filter: blur(10px);
  z-index: 5;
  border-radius: 10px;
  .progressBar {
    border-radius: 10px;
    height: 100%;
    width: 90%;
    background: white;
  }
}
</style>
