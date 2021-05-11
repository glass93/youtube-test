<template>
  <li @click="selectVideo">
    <!-- <div v-html="video.snippet.title"></div> -->
    <img :src="youtubeThumbnailSrc" alt="youtube-thumbnail-image">
    <div class="video-title">{{ video.snippet.title | stringUnescape }}</div>
  </li>
</template>

<script>
import _ from 'lodash'

export default {
  name: 'VideoListItem',
  props: {
    video: {
      type: Object
    }
  },
  methods: {
    selectVideo() {
      this.$emit('select-video', this.video)
    }
  },
  computed: {
    youtubeThumbnailSrc() {
      return this.video.snippet.thumbnails.default.url
    }
  },
  filters: {
    stringUnescape(rawText) {
      return _.unescape(rawText)
    }
  }
}
</script>

<style scoped>
li {
  display: flex;
  padding: 10px 0;
}

.video-title {
  margin-left: 10px;
}
</style>
