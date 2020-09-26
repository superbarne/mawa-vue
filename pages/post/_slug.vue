<template>
  <div>
    <b-container>
      <ArticleDetail :post="post" />
    </b-container>
  </div>
</template>
<script>
import { createClient } from '~/plugins/contentful.js'

const client = createClient()

export default {
  async asyncData ({ env, params: { slug } }) {
    const { items: [post] } = await client.getEntries({
      content_type: 'post',
      'fields.slug[in]': slug
    })

    return {
      post
    }
  }
}
</script>
