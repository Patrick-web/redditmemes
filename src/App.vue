<template>
  <div id="app">
    <!-- <Timeout /> -->
    <div class="memes">
      <MemeCard v-for="meme in memes" :key="meme.id" :imageSrc="meme.source" />
    </div>
    <vs-button
      style="position:fixed;bottom:50px;z-index:10"
      circle
      icon
      floating
      @click="showSettings = !showSettings"
    >
      <img width="20px" src="@/assets/settings-outline.svg" alt="" />
    </vs-button>
    <vs-dialog v-model="showSettings">
      <div class="formGroup adder">
        <label id="adderlabel">Add Subreddit</label>
        <vs-input
          v-model="newSubreddit"
          placeholder="eg r/somthingthatsactuallyfunny"
        />
        <vs-button @click="addSubreddit" block>Add</vs-button>
      </div>
      <div class="formGroup">
        <label for="">Max Results</label>
        <vs-select placeholder="Max Results 20" v-model="maxResults">
          <vs-option label="20" value="20">
            20
          </vs-option>
          <vs-option label="30" value="30">
            30
          </vs-option>
          <vs-option label="40" value="40">
            40
          </vs-option>
          <vs-option label="50" value="50">
            50
          </vs-option>
          <vs-option label="60" value="60">
            60
          </vs-option>
          <vs-option label="70" value="70">
            70
          </vs-option>
          <vs-option label="80" value="80">
            80
          </vs-option>
        </vs-select>
      </div>
      <div class="formGroup">
        <label for="">Fullscreen</label>
        <vs-switch @click="toggleFullScreen" v-model="fullscreen" />
      </div>
      <div class="formGroup">
        <a href="https://twitter.com/home">🐔 My Twitter</a>
      </div>
      <div class="formGroup">
        <i>Long press on the images to see more options</i>
      </div>
    </vs-dialog>
    <Pills
      v-on:moreMemes="addMemes"
      v-on:memes="getFirstMemes"
      msg="Welcome to Your Vue.js App"
      :maxResults="maxResults"
      :newSubreddits="newSubreddits"
    />
  </div>
</template>

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
      showSettings: false,
      maxResults: "20",
      fullscreen: false,
      newSubreddit: "",
      newSubreddits: [],
    };
  },
  methods: {
    addSubreddit() {
      this.newSubreddits.unshift(this.newSubreddit.replace("r/", ""));
      const notify = this.$vs.notification({
        text: `r/${this.newSubreddit} added`,
        position: "top-left",
        color: "success",
      });
      this.newSubreddit = "";
    },
    toggleFullScreen() {
      if (!this.fullscreen) {
        document.body
          .requestFullscreen()
          .then(() => {})
          .catch(() => {
            const notify = this.$vs.notification({
              text: `Cannot go fullscreen 🤥`,
              position: "top-left",
              color: "danger",
            });
          });
      } else {
        document.exitFullscreen();
      }
    },
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
    window.addEventListener("offline", () => {
      const notify = this.$vs.notification({
        text: "I need internet to feed  you memes!",
        position: "top-left",
        color: "danger",
        duration: 1000,
      });
    });
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
.vs-dialog {
  filter: invert(1) hue-rotate(180deg);
}
.formGroup {
  padding: 10px;
  border-bottom: 1px solid rgba(0, 0, 0, 0.089);
  .vs-switch {
    margin-top: 10px;
    max-width: 50px;
  }
  .vs-select-content {
    margin-top: 10px;
  }
  a {
    text-decoration: none;
  }
}
.adder {
  input {
    width: 100%;
  }
  .vs-input {
    margin-top: 5px;
    margin-bottom: 5px;
  }
  #adderlabel {
    margin-left: 10px;
  }
}
@media (min-width: 1000px) {
  ::-webkit-scrollbar {
    width: 10px;
    // background: #008cff;
  }
  .memes {
    width: 900px;
    margin: auto;
  }
  .Pills {
    width: 900px;
    margin: auto;
    left: 50%;
    transform: translateX(-50%);
  }
  .MemeCard {
    max-height: 90vh;
    margin-bottom: 20px;
  }
}
</style>
