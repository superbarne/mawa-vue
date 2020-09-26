<template>
  <b-container>
    <h1>Kategorie</h1>
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
      order: '-sys.createdAt'
    })

    return {
      posts
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
        order: '-sys.createdAt'
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
