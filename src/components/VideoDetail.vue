<template>
  <div>
    <iframe 
      :src="youtubeSrc" 
      frameborder="0"  
      width="640" 
      height="360">
    </iframe>
    <h2>{{ video.snippet.title | stringUnescape }}</h2>
    <p>{{ video.snippet.description | stringUnescape }}</p>
  </div>
</template>

<script>
import _ from 'lodash'

export default {
  name: 'VideoDetail',
  props: {
    video: {
      type: Object
    }
  },
  computed: {
    youtubeSrc() {
      return `https://www.youtube.com/embed/${this.video.id.videoId}`
    }
  },
  filters: {
    stringUnescape(rawText) {
      return _.unescape(rawText)
    }
  }
}
</script>

<style>

</style>
