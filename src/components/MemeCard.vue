<template>
  <div class="MemeCard">
    <div class="memeArea">
      <img class="memeImage" :src="imageSrc" alt="" />
      <div class="skeleton">
        <p>Waiting for the high res meme....</p>
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
  position: relative;
  background: rgb(34, 34, 34);
  color: white;
  margin-bottom: 20px;
  .memeArea {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    .memeImage {
      object-fit: contain;
      margin: auto;
      max-width: 95%;
      border-radius: 10px;
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
