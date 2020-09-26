<template>
  <div class="article-meta">
    <ul>
      <li>
        <i class="fas fa-clock" />
        <span>
          {{ formatedCreatedAt }}
        </span>
      </li>
      <li v-if="profiles.length > 0">
        <i class="fas fa-star" />
        <nuxt-link v-for="profile in profilesFiltered" :key="profile.sys.id" :to="`/profile/${profile.fields.type}/${profile.fields.slug}`">
          {{ profile.fields.name }}
        </nuxt-link>
      </li>
      <li v-if="categories.length > 0">
        <i class="fas fa-tags" />
        <nuxt-link v-for="category in categories" :key="category.sys.id" :to="`/tag/${category.fields.slug}`">
          {{ category.fields.name }}
        </nuxt-link>
      </li>
    </ul>
  </div>
</template>

<style lang="scss">
  @import "./ArticleMetaBar.scss";
</style>

<script>
import 'dayjs/locale/de'
import dayjs from 'dayjs'
dayjs.locale('de')
export default {
  props: {
    categories: {
      type: Array,
      required: false,
      default: () => []
    },
    profiles: {
      type: Array,
      required: false,
      default: () => []
    },
    createdAt: {
      type: String,
      required: false,
      default: () => null
    }
  },
  computed: {
    profilesFiltered () {
      return this.profiles.filter(item => item.fields)
    },
    formatedCreatedAt () {
      return dayjs(this.createdAt).format('DD MMM YYYY')
    }
  }
}
</script>
