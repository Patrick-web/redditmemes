<template>
  <div id="app">
    <div class="memes">
      <MemeCard v-for="meme in memes" :key="meme.id" :imageSrc="meme.source" />
    </div>
    <Pills v-on:memes="populateData" msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
import Pills from "./components/Pills.vue";
import MemeCard from "./components/MemeCard.vue";

export default {
  name: "App",
  data() {
    return {
      memes: [],
    };
  },
  methods: {
    populateData(memes) {
      this.memes = memes;
    },
  },
  components: {
    Pills,
    MemeCard,
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}
body {
  background: black;
}
.memes {
  scroll-snap-type: mandatory;
}
</style>
