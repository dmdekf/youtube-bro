<template>
  <div>
    <li class="list-group-item">
      <img :src="thumbnailUrl" />
      <div class="media-body">
        <span v-html="video.snippet.title"></span>
      </div>
    </li>
  </div>
</template>

<script>
export default {
  name: "VideoListItem",
  props: {
    video: Object,
  },
  computed: {
    thumbnailUrl() {
      return this.video.snippet.thumbnails.default.url;
    },
  },
};
</script>

<style scoped>
li {
  display: flex;
  cursor: pointer;
}

li:hover {
  background-color: #eee;
}

.media-body {
  margin: auto 0;
}
</style>
