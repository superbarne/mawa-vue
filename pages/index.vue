<template>
  <b-container>
<<<<<<< HEAD
    <ArticleSlider />
    <ArticleTeaser />
    <pre>{{ posts }}</pre>
=======
    <ArticleTeaser v-for="post in posts" :key="post.sys.id" :post="post" />
    <infinite-loading @infinite="infiniteHandler" />
>>>>>>> 21711cf1181ad65487d2f6affd4c57002339cecf
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
