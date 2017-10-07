<template>
  <div class="video-band">
    <header>
      <h1>some {{ randomWord }} videos</h1>
    </header>
    <div ref="band" class="band">
      <button class="band-prev" @click="prev">«</button>
      <VideoBox v-for="(video,i) in videos"
        ref="video"
        :key="i"
        :title="video.title"
        :duration="video.duration"
        :thumbnail="video.thumbnail"
      />
      <button class="band-next" @click="next">»</button>
    </div>
  </div>
</template>

<script>
import VideoBox from './VideoBox.vue'

export default {
  props: [ 'videos' ],
  components: { VideoBox },
  data () {
    return {
      index: 0 // video at this index is the first shown
    }
  },
  computed: {
    bodyWidth () {
      return document.body.offsetWidth
    },
    videoWidth () {
      return this.$refs.video[0].$el.offsetWidth + 32
    },
    threshold () {
      const n = ~~(this.bodyWidth / this.videoWidth)
      return this.videos.length - n
    },
    randomWord () {
      const words = ['gorgeous', 'awesome', 'beautiful', 'motivating', 'hilarious', 'fascinating']
      return words[~~(Math.random() * words.length)]
    }
  },
  methods: {
    prev () { this.index > 0 ? this.index-- : 0 },
    next () { this.index < this.threshold ? this.index++ : this.threshold },
  },
  watch: {
    index (newValue, oldValue) {
      const offset = this.videoWidth * newValue
      this.$refs.band.style.marginLeft = `-${offset}px`
    }
  }
}
</script>

<style scoped>
.video-band > header > h1 {
  position: relative;
  text-align: left;
  margin: 0 0 -1em 0;
  padding: 0 .5em;
}
.band {
  display: flex;
  flex-flow: row nowrap;
  justify-content: flex-start;
  margin: 2em 0;
  height: 260px;
  transition: margin .5s ease-out;
}
.band > button {
  display: none;
  position: absolute;
  height: 260px;
  border: none;
  background: rgba(0, 0, 0, .3);
  color: white;
  text-shadow: 0 0 4px black;
  padding: 0 .5em;
  font-size: 2em;
  z-index: 1;
}
.band:hover > button {
  display: block;
}
.band > button:hover {
  background: rgba(0, 0, 0, .8);
}
.band-prev {
  left: 0;
}
.band-next {
  right: 0;
}
</style>
