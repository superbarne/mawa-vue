<template>
  <div>
    <div v-if="play" class="youtube-player done">
      <iframe frameBorder="0" allowFullscreen="" :src="`https://www.youtube.com/embed/${videoId}?rel=0&showinfo=0&autoplay=1`" />
    </div>
    <div v-if="!play" class="youtube-player done" @click="play = true">
      <div class="play-button" />
      <img :src="`http://img.youtube.com/vi/${videoId}/maxresdefault.jpg`">
    </div>
  </div>
</template>
<script>
export default {
  props: {
    uri: {
      required: true,
      type: String
    }
  },
  data () {
    return {
      play: false
    }
  },
  computed: {
    videoId () {
      return this.uri.split('/').slice(-1)[0]
    }
  }
}
</script>
<style lang="scss">
@import './ArticleVideoYoutube.scss';
</style>
