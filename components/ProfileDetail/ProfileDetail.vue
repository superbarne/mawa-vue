<template>
  <div class="profile-detail">
    <div class="profile-detail__cover">
      <img src="https://via.placeholder.com/1080x400" alt="Image" class="profile-detail__cover-media">
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
      </b-col>
      <b-col cols="12" md="4">
        <div class="sidebar">
          <div class="profile-detail__socials">
            <a v-if="profile.fields.instagram" class="btn instagram" href="/">Instagram</a>
            <a v-if="profile.fields.twitter" class="btn twitter" href="/">Twitter</a>
            <a v-if="profile.fields.youtube" class="btn youtube" href="/">YouTube</a>
            <a v-if="profile.fields.vimeo" class="btn vimeo" href="/">Vimeo</a>
          </div>
          Sidebar
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
  }
}
</script>
