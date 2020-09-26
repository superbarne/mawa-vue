<template>
  <b-container>
    <h1>{{ category.fields.name }}</h1>
    <ArticleTeaser v-for="post in posts" :key="post.sys.id" :post="post" />
    <infinite-loading @infinite="infiniteHandler" />
  </b-container>
</template>

<script>
import { createClient } from '~/plugins/contentful.js'
const client = createClient()
const limit = 3
export default {
  async asyncData ({ env, params: { slug } }) {
    const { items: [category] } = await client.getEntries({
      content_type: 'category',
      'fields.slug[in]': slug
    })
    const { items: posts } = await client.getEntries({
      content_type: 'post',
      limit,
      order: '-sys.createdAt',
      'fields.categories.sys.id': category.sys.id
    })

    return {
      posts,
      category
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
        order: '-sys.createdAt',
        'fields.categories.sys.id': this.category.sys.id
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
