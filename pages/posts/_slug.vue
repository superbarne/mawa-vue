<template>
  <pre>{{ post }}</pre>
</template>
<script>
import { createClient } from '~/plugins/contentful.js'
const client = createClient()

export default {
  async asyncData ({ env, params: { slug } }) {
    const { items: posts } = await client.getEntries({
      content_type: 'post',
      'fields.slug[in]': slug
    })

    return {
      posts
    }
  }
}
</script>
