<template>
  <div v-if="videos" class="col-lg-4">
    <!-- <h1 class="display-5">Video LIST</h1> -->
    <!-- <ul>
      <li v-for="video in videos" :key="video.etag">
        <img :src="video.snippet.thumbnails.default.url" alt="image thumbnails" />
        {{ video.snippet.title }}
      </li>
    </ul>-->
    <ul class="list-group">
      <VideoListItem
        @video-select="onVideoSelect"
        :video="video"
        v-for="video in videos"
        :key="video.etag"
      />
    </ul>
  </div>
</template>

<script>
import VideoListItem from "./VideoListItem";

export default {
  name: "VideoList",
  components: {
    // 키와 벨류 값이 같다면 한번만 쓸 수 있다.
    VideoListItem
  },
  props: {
    videos: Array
  },
  methods: {
    //이름이 중복되어도 상관없다. 분리, 독립된 컴포넌트.
    //컴포넌트 간은 느슨한 연결이다.
    onVideoSelect(video) {
      this.$emit("video-select", video);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style></style>
