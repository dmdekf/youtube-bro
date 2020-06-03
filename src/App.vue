<template>
  <div class="container">
    <!-- emit 2. 듣고, "a" -->
    <SearchBar @input-change="onInputChange" />
    <VideoList :videos="videos" />
  </div>
</template>

<script>
import axios from 'axios'

import SearchBar from './components/SearchBar.vue'
import VideoList from './components/VideoList.vue'

const API_KEY = process.env.VUE_APP_YOUTUBE_API_KEY  // 비활성화된 키
const API_URL = 'https://www.googleapis.com/youtube/v3/search'

export default {
  name: 'App',
  components: { SearchBar, VideoList, },
  data() {
    return {
      inputValue: '',
      videos: [],
    }
  },
  methods: {
    onInputChange(inputText) {
      this.inputValue = inputText
      // console.log(API_KEY)

      axios.get(API_URL, {
        params: {
          key: API_KEY,
          part: 'snippet',
          type: 'video',
          q: this.inputValue,
          maxResults: 10
        }
      })
        .then(res => this.videos = res.data.items)
        .catch(err => console.error(err))
    },
  }
}
</script>

<style>

</style>
