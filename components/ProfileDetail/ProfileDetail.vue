<template>
  <div class="profile-detail">
    <div class="profile-detail__cover">
      <img src="https://via.placeholder.com/1080x400" alt="Image" class="profile-detail__cover-media">
      <div class="profile-detail__cover-caption">
        <h3 class="profile-detail__cover-title">
          Fahrer
        </h3>
      </div>
    </div>
    <b-row>
      <b-col cols="12" md="8">
        <ArticleTeaser v-for="post in posts" :key="post.sys.id" :post="post" />
        <infinite-loading @infinite="$emit('posts-load-more', $event)" />
      </b-col>
      <b-col cols="12" md="4">
        <div class="sidebar">
          Sidebar
          <div
            v-if="profile.fields.facebook"
            class="fb-page item facebook"
            :data-href="profile.fields.facebook"
            data-width="480"
            data-hide-cover="false"
            data-show-facepile="false"
            data-show-posts="true"
            height="800px"
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
  }
}
</script>
