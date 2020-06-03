<template>
  <div v-if="selectedVideo" class="col-lg-8">
    <div class="embed-responsive embed-responsive-16by9">
      <iframe class="embed-responsive-item" :src="videoUrl" allowfullscreen></iframe>
    </div>
    <div class="details">
      <!-- inner HTML -->
      <!-- <h4 v-html="selectedVideo.snippet.title"></h4> -->
      <h4>{{ selectedVideo.snippet.title}}</h4>
      <!-- inner text -->
      <p>{{ selectedVideo.snippet.description }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "VideoDetail",
  props: {
    selectedVideo: Object
  },
  computed: {
    videoUrl() {
      return `https://www.youtube.com/embed/${this.selectedVideo.id.videoId}`;
    }
  }
};
</script>

<style scoped>
div.details {
  margin-top: 10px;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
}
</style>