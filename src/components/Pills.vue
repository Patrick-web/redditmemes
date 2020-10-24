<template>
  <div class="Pills">
    <span
      v-for="subreddit in subreddits"
      :key="subreddit"
      @click="switchActivePill($event, subreddit)"
      class="pill"
      >r/{{ subreddit }}</span
    >
  </div>
</template>

<script>
export default {
  data() {
    return {
      subreddits: [
        "programminghumor",
        "dankmemes",
        "memes",
        "terriblefacebookmemes",
        "dndmemes",
        "Animemes",
        "DeepFriedMemes",
        "bikinibottomtwitter",
        "trippinthroughtime",
        "anime_irl",
        "data_irl",
        "blackpeopletwitter",
        "whitepeopletwitter",
        "boottoobig",
        "bonehurtingjuice",
        "historymemes",
        "musicmemes",
        "kenm",
        "meow_irl",
        "woof_irl",
        "prequelmemes",
        "sequelmemes",
        "OTmemes",
        "youdontsurf",
        "starterpacks",
      ],
    };
  },
  methods: {
    switchActivePill(e, subreddit) {
      document.querySelector(".activePill").classList.remove("activePill");
      e.target.classList.add("activePill");
      document.body.scrollTop = 0;
      this.memeFetcher(subreddit);
    },
    memeFetcher(subreddit) {
      const loading = this.$vs.loading({
        text: "Relaaax. Let me help you waste time,ok",
        background: "black",
      });
      fetch(`https://www.reddit.com/r/${subreddit}/new.json`)
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
            memes.push(image);
          });
          memes.shift();
          this.$emit("memes", memes);
        })
        .catch(function(err) {
          console.log(err); // Log error if any
        });
    },
  },
};
</script>

<style lang="scss">
.Pills {
  position: fixed;
  bottom: 0;
  padding: 15px;
  width: 100vw;
  overflow-x: scroll;
  background: #00000054;
  backdrop-filter: blur(20px);
  .pill {
    margin: 10px;
    background: #ffffff1c;
    border-radius: 20px;
    padding: 5px;
    padding-right: 10px;
    padding-left: 10px;
    color: white;
  }
  .activePill {
    background: #008cff !important;
  }
}
</style>
