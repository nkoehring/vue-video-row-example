<template>
  <div id="app">
    <VideoBand :key="i" :videos="videos" v-for="(videos,i) in videoBands" />
  </div>
</template>

<script>
import VideoBand from './components/VideoBand.vue'
import thumbnail01 from './assets/thumb01.jpg'
import thumbnail02 from './assets/thumb02.jpg'
import thumbnail03 from './assets/thumb03.jpg'
import thumbnail04 from './assets/thumb04.jpg'
import thumbnail05 from './assets/thumb05.jpg'
import thumbnail06 from './assets/thumb06.jpg'

const thumbnails = [
  thumbnail01,
  thumbnail02,
  thumbnail03,
  thumbnail04,
  thumbnail05,
  thumbnail06
]

export default {
  name: 'app',
  components: { VideoBand },
  data () {
    return {
      videoBands: []
    }
  },
  beforeMount () {
    // beforeMount runs before the component is put into the DOM
    // this function creates three "video bands", arrays of video objects.
    let n = 3

    while (n--) {
      // create an array of n videos where n is a random number between 5..20
      // notice: ~~ is 2× bitwise NOT which has Math.floor as side effect
      let l = 5 + ~~(Math.random() * 15)
      let videoBand = new Array(l)

      for(; l>=0; l--) {
        const t = ~~(Math.random() * thumbnails.length)
        videoBand[l] = { thumbnail: thumbnails[t], title: 'motivating video', duration: 320 }
      }
      this.videoBands.push(videoBand)
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
