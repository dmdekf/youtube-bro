<template>
  <div>
    <h1 class="display-3">VideoList</h1>
    <ul class="list-group">
      <VidioListItem v-for="video in videos" :key="video.etag" :video="video" />
    </ul>
  </div>
</template>

<script>
import VidioListItem from "./VideoListItem";
export default {
  name: "VideoList",
  components: {
    VidioListItem,
  },
  props: {
    videos: Array,
  },
};
</script>

<style></style>
