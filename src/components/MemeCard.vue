<template>
  <div class="MemeCard">
    <img class="blurImage" :src="imageSrc" alt="" />
    <div class="memeArea">
      <img :src="imageSrc" alt="" />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    imageSrc: String,
  },
};
</script>

<style lang="scss">
.MemeCard {
  width: 100vw;
  height: 100vh;
  position: relative;
  .blurImage {
    position: absolute;
    width: 100%;
    height: 100%;
    filter: blur(5px);
    opacity: 0.5;
  }
  .memeArea {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    img {
      margin: auto;
      width: 95%;
      border-radius: 10px;
      position: absolute;
    }
  }
}
</style>
