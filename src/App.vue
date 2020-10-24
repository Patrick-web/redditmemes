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
      console.log(memes);
      this.memes = memes;
    },
  },
  components: {
    Pills,
    MemeCard,
  },
  mounted() {
    document.querySelector(".pill").classList.add("activePill");
    const loading = this.$vs.loading({ text: "Fetching them memes Bouy!!!" });
    fetch(`https://www.reddit.com/r/programminghumor/new.json`)
      .then((res) => {
        return res.json(); // Convert the data into JSON
      })
      .then((res) => {
        loading.close();
        const postsArr = res.data.children;
        const memes = [];
        postsArr.forEach((post) => {
          const image = {
            id: Math.random()
              .toString(12)
              .substring(0),
            source: post.data.url,
          };
          this.memes.push(image);
        });
        this.memes.shift();
      })
      .catch(function(err) {
        console.log(err); // Log error if any
      });
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
  max-width: 500px;
}
</style>
