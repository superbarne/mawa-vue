<template>
  <div class="profile-detail">
    <div class="profile-detail__cover">
      <img v-if="headerImage" :src="headerImage" alt="Image" class="profile-detail__cover-media">
      <div class="profile-detail__cover-caption">
        <h3 class="profile-detail__cover-title">
          {{ profile.fields.name }}
        </h3>
      </div>
    </div>
    <b-row>
      <b-col cols="12" md="8">
        <pre>{{ profile }}</pre>
        <ArticleTeaser v-for="post in posts" :key="post.sys.id" :post="post" />
        <infinite-loading @infinite="$emit('posts-load-more', $event)" />
      </b-col>
      <b-col cols="12" md="4">
        <div class="sidebar">
          <div class="profile-detail__socials">
            <a v-if="profile.fields.website" class="btn website" :href="profile.fields.website" target="_blank">Website</a>
            <a v-if="profile.fields.instagram" class="btn instagram" :href="profile.fields.instagram" target="_blank">Instagram</a>
            <a v-if="profile.fields.twitter" class="btn twitter" :href="profile.fields.twitter" target="_blank">Twitter</a>
            <a v-if="profile.fields.youtube" class="btn youtube" :href="profile.fields.youtube" target="_blank">YouTube</a>
            <a v-if="profile.fields.vimeo" class="btn vimeo" :href="profile.fields.vimeo" target="_blank">Vimeo</a>
          </div>
          <div
            v-if="profile.fields.facebook"
            class="fb-page item facebook"
            :data-href="profile.fields.facebook"
            data-width="480"
            data-hide-cover="false"
            data-show-facepile="false"
            data-show-posts="true"
            height="900px"
          />
        </div>
      </b-col>
    </b-row>
  </div>
</template>

<style lang="scss">
  @import "./ProfileDetail.scss";
</style>

<script>

export default {
  props: {
    profile: {
      type: Object,
      required: true
    },
    posts: {
      type: Array,
      default: () => []
    }
  },
  computed: {
    headerImage () {
      const content = this.profile.fields.content.content
      if (!content[0]) { return null }
      const hyperlink = content[0].content.find(item => item.nodeType === 'hyperlink')
      if (hyperlink) {
        if (hyperlink.data.uri.includes('s3.eu-central')) {
          return hyperlink.data.uri
        }
      }
      return null
    }
  }
}
</script>
