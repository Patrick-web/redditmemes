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
        "hmmm",
        "MemeEconomy",
        "thanosdidnothingwrong",
        "blackpeopletwitter",
        "whitepeopletwitter",
        "boottoobig",
        "bonehurtingjuice",
        "historymemes",
        "musicmemes",
        "kenm",
        "prequelmemes",
        "sequelmemes",
        "OTmemes",
        "youdontsurf",
        "starterpacks",
        "ohffensivememes",
      ],
    };
  },
  methods: {
    switchActivePill(e, subreddit) {
      if (document.querySelector(".activePill")) {
        document.querySelector(".activePill").classList.remove("activePill");
      }
      e.target.classList.add("activePill");
      document.body.scrollTop = 0;
      this.fetchNew(subreddit);
    },
    fetchNew(subreddit) {
      const loading = this.$vs.loading({
        text: "Relaaax. Let me help you waste time,ok",
        background: "#141417",
        type: "waves",
      });
      fetch(`https://www.reddit.com/r/${subreddit}/new.json?limit=100`)
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
          this.$emit("memes", memes, subreddit);
        })
        .catch(function(err) {
          loading.close();
          console.log(err); // Log error if any
        });
    },
  },
};
</script>

<style lang="scss">
.Pills {
  position: fixed;
  z-index: 10;
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
