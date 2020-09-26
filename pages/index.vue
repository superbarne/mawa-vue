<template>
  <b-container>
    <ArticleSlider :slider-posts="sliderPosts" />
    <ArticleTeaser v-for="post in posts" :key="post.sys.id" :post="post" />
    <infinite-loading @infinite="infiniteHandler" />
  </b-container>
</template>

<script>
import { createClient } from '~/plugins/contentful.js'
const client = createClient()
const limit = 3
export default {
  async asyncData ({ env }) {
    const { items: posts } = await client.getEntries({
      content_type: 'post',
      limit,
      order: '-fields.createdAt'
    })

    const sliderCatagoryId = '563e3302f6b2ab1d1a18938c'
    const { items: sliderPosts } = await client.getEntries({
      content_type: 'post',
      'fields.categories.sys.id': sliderCatagoryId
    })

    return {
      posts,
      sliderPosts
    }
  },
  data () {
    return {
      skip: 0
    }
  },
  methods: {
    async infiniteHandler ($state) {
      this.skip += limit
      const { items: posts } = await client.getEntries({
        content_type: 'post',
        limit,
        skip: this.skip,
        order: '-fields.createdAt'
      })
      if (posts.length) {
        this.posts.push(...posts)
        $state.loaded()
      } else {
        $state.complete()
      }
    }
  }
}
</script>
