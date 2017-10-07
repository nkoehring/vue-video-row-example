<template>
  <div class="video-box">
    <header>
      {{ title }}
      <span class="duration">{{ durationInMinutes }}</span>
    </header>
    <img :src="thumbnail" :alt="`${title} (${durationInMinutes})`" />
  </div>
</template>

<script>
import VideoBox from './VideoBox.vue'

export default {
  props: [ 'title', 'duration', 'thumbnail' ],
  computed: {
    durationInMinutes () {
      const minutes = ~~(this.duration / 60.0)
      const seconds = this.duration - minutes * 60

      return `${minutes}:${seconds}`
    }
  }
}
</script>

<style scoped>
  .video-box {
    position: relative;
    margin: 1em;
    padding: 0 1em;
  }
  .video-box:hover {
    background-color: #EEE;
  }
  .video-box > img {
    width: 400px;
  }
  .video-box > header {
    position: absolute;
    bottom: 2em;
    left: 0;
    width: 100%;
    display: block;
    background: rgba(0,0,0,.75);
    color: white;
    height: 2em;
    line-height: 2em;
    margin-bottom: -2em;
  }
</style>
