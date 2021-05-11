<template>
  <div>
    <ul>
      <VideoListItem 
        v-for="video in videos" 
        :key="video.id.videoId"
        :video="video"
        @select-video="selectVideo"
      />
    </ul>
  </div>
</template>

<script>
import VideoListItem from './VideoListItem'

export default {
  name: 'VideoList',
  components: {
    VideoListItem
  },
  methods:{
    selectVideo(value) {
      this.$emit('select-video', value)
    }
  },
  props: {
    videos: {
      type: Array
    }
  }
}
</script>

<style scoped>
ul {
  list-style: none;
}
</style>
