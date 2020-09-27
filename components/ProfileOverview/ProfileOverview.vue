<template>
  <div class="profile-overview">
    <div v-if="categories.length > 0" class="profile-overview__filter">
      <nuxt-link :to="`/profile/${type}`" class="btn">
        Alle
      </nuxt-link>
      <nuxt-link v-for="category in categories" :key="category.sys.id" class="btn" :to="`/profile/${type}/category/${category.fields.slug}`">
        {{ category.fields.name }}
      </nuxt-link>
    </div>
    <b-row>
      <ProfileTeaser v-for="profile in profiles" :key="profile.sys.id" class="col-12 col-sm-6 col-lg-4" :profile="profile" />
    </b-row>
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
