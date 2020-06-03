<template>
  <div class="container">
    <!-- emit 2. 듣고, "a" -->
    <SearchBar @input-change="onInputChange" />
    <div class="row">
      <VideoDetail :selectedVideo="selectedVideo" />
      <VideoList @video-select="onVideoSelect" :videos="videos" />
      <VideoPlay :videos="videos" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import SearchBar from "./components/SearchBar";
import VideoList from "./components/VideoList";
import VideoDetail from "./components/VideoDetail";
const API_KEY = process.env.VUE_APP_YOUTUBE_API_KEY;
const API_URL = "https://www.googleapis.com/youtube/v3/search";

export default {
  name: "App",
  components: {
    SearchBar,
    VideoList,
    VideoDetail
  },
  data() {
    return {
      inputValue: "",
      videos: null,
      selectedVideo: null
    };
  },
  methods: {
    onInputChange(inputText) {
      console.log(`input-change이벤트발생 : ${inputText}`);
      this.inputValue = inputText;
      axios
        .get(API_URL, {
          params: {
            key: API_KEY,
            part: "snippet",
            type: "video",
            q: this.inputValue,
            maxResults: 4
          }
        })
        .then(res => {
          res.data.items.forEach(item => {
            // html 내부 &#1234 를 처리, v-html 대신.
            const parser = new DOMParser();
            const doc = parser.parseFromString(item.snippet.title, "text/html");
            item.snippet.title = doc.body.innerText;
          });
          this.videos = res.data.items;
        })
        .catch(err => console.error(err));
    },
    onVideoSelect(video) {
      this.selectedVideo = video;
    }
  }
};
</script>

<style>
</style>
