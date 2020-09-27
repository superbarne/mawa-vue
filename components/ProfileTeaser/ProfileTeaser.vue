<template>
  <nuxt-link class="profile-teaser" :to="`/profile/${profile.fields.type}/${profile.fields.slug}`">
    <div class="profile-teaser__cover">
      <img v-if="headerImage" :src="headerImage" alt="Image" class="profile-teaser__cover-media">
      <div class="profile-teaser__cover-caption">
        <h3 class="profile-teaser__cover-title">
          {{ profile.fields.name }}
        </h3>
      </div>
    </div>
  </nuxt-link>
</template>

<style lang="scss">
  @import "./ProfileTeaser.scss";
</style>

<script>
export default {
  props: {
    profile: {
      type: Object,
      required: true
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
