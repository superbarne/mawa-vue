<template>
  <div class="profile-overview">
    <div class="profile-overview__filter">
      <nuxt-link v-for="category in categories" :key="category.sys.id" class="btn" :to="`/profile/${type}/category/${category.fields.slug}`">
        {{ category.fields.name }}
      </nuxt-link>
    </div>
    <div v-for="profile in profiles" :key="profile.sys.id">
      <ProfileTeaser :profile="profile" />
    </div>
  </div>
</template>

<style lang="scss">
@import "./ProfileOverview.scss";
</style>

<script>
export default {
  props: {
    profiles: {
      type: Array,
      required: true
    },
    categories: {
      type: Array,
      required: true
    },
    type: {
      type: String,
      required: true
    }
  }
}
</script>
