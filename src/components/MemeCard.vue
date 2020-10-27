<template>
  <div class="MemeCard">
    <!-- <img class="blurImage" :src="imageSrc" alt="" /> -->
    <div class="memeArea">
      <img class="memeImage" :src="imageSrc" alt="" />
      <div class="skeleton">
        <p>Waiting for the high res meme</p>
      </div>
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
  scroll-snap-align: center;
  .blurImage {
    position: absolute;
    top: 0;
    width: 100%;
    height: 100%;
    filter: blur(30px);
    opacity: 0.2;
  }
  .memeArea {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    .memeImage {
      margin: auto;
      width: 95%;
      border-radius: 10px;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      z-index: 3;
    }
  }
  .skeleton {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
}
@media (min-width: 700px) {
  .MemeCard {
    width: 50%;
    margin: auto;
    transform: scale(0.8);
  }
}
</style>
