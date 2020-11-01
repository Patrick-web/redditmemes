<template>
  <div id="app">
    <!-- <Timeout /> -->
    <div class="memes">
      <MemeCard v-for="meme in memes" :key="meme.id" :imageSrc="meme.source" />
    </div>
    <Pills
      v-on:moreMemes="addMemes"
      v-on:memes="getFirstMemes"
      msg="Welcome to Your Vue.js App"
    />
  </div>
/template>

<script>
import Pills from "./components/Pills.vue";
import MemeCard from "./components/MemeCard.vue";
import Timeout from "./components/Timeout.vue";

export default {
  name: "App",
  data() {
    return {
      memes: [],
      currentSubreddit: "",
      currentFetch: 0,
    };
  },
  methods: {
    getFirstMemes(memes, subreddit) {
      this.currentSubreddit = subreddit;
      this.currentFetch = 0;
      console.log(memes);
      this.memes = memes;
    },
    addMemes(newMemes) {
      newMemes.forEach((meme) => {
        this.memes.push(meme);
      });
    },
    getMoreMemes() {
      switch (this.currentFetch) {
        case 0:
          this.fetchRising();
          break;
        case 1:
          this.fetchRandom();
          break;
        case 2:
          this.fetchControversial();
          break;
        case 3:
          this.fetchHot();
          break;
        default:
          console.log(this.currentFetch);
          console.log("Some Impossible error happened");
          break;
      }
      this.currentFetch += 1;
    },
  },
  components: {
    Pills,
    MemeCard,
    Timeout,
  },
  mounted() {
    document.querySelector(".pill").click();
  },
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}
body {
  background: black;
  overflow: hidden;
}
.memes {
  scroll-snap-type: y proximity;
  scroll-padding-bottom: 0vh;
  overflow-y: scroll;
  height: 100vh;
}
#fetchMoreBt {
  font-weight: 800;
  background: #008cff;
  margin: auto;
  display: flex;
  align-items: center;
  position: relative;
  z-index: 20;
  img {
    width: 30px;
    margin-left: 20px;
  }
}
</style>
