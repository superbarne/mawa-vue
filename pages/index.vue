<template>
  <b-container>
    <ArticleTeaser />
    <pre>{{ posts }}</pre>
  </b-container>
</template>

<script>
import { createClient } from '~/plugins/contentful.js'
const client = createClient()

export default {
  async asyncData ({ env }) {
    const { items: posts } = await client.getEntries({
      content_type: 'post',
      order: '-sys.createdAt'
    })

    return {
      posts
    }
  }
}
</script>
