<template>
  <div id="app">
    <header>
      <SearchBar 
        :inputText="inputText"
        @input-change="inputChange"
      />
    </header>
    <section>
      <div class="main-container">
        <VideoDetail
          v-if="selectedVideo"
          :video="selectedVideo"
        />
        <div v-else>선택된 영상이 없습니다</div>
        <VideoList
          :videos="videos"
          @select-video="selectVideo"
        />
      </div>
    </section>
  </div>
</template>

<script>
import axios from 'axios'
import SearchBar from '@/components/SearchBar'
import VideoList from '@/components/VideoList'
import VideoDetail from '@/components/VideoDetail'

export default {
  name: 'App',
  data() {
    return {
      inputText: '',
      videos: [],
      selectedVideo: null
    }
  },
  components: {
    SearchBar,
    VideoList,
    VideoDetail
  },
  methods: {
    inputChange(value) {
      // console.log(value)
      this.inputText = value
      // console.log(process.env.VUE_APP_YOUTUBE_API_KEY)
      const params = {
        // 필수
        key: process.env.VUE_APP_YOUTUBE_API_KEY,
        part: 'snippet',
        // 옵션
        q: this.inputText,
        type: 'video'
      }
      // API 요청
      // axios({
      //   method: 'get',
      //   url: 'https://www.googleapis.com/youtube/v3/search',
      //   params
      // })
      axios.get(
        'https://www.googleapis.com/youtube/v3/search', 
        { params }
      )
        .then(res => {
          console.log(res)
          this.videos = res.data.items
          this.selectedVideo = this.videos[0]
        })
        .catch(err => {
          console.error(err)
        })
    },
    selectVideo(value) {
      console.log(value)
      this.selectedVideo = value
    }
  }
}
</script>

<style scoped>
#app {
  width: 100vw;
}

header {
  display: flex;
  justify-content: center;
  margin: 20px;
}

section {
  display: flex;
  justify-content: center;
  width: 100%;
}

.main-container {
  display: flex;
  justify-content: center;
  width: 80%;
}
</style>
