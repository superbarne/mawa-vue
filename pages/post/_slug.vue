<template>
  <div>
    <RichTextRenderer v-if="post" :document="post.fields.content" />
    <pre>{{ post }}</pre>
  </div>
</template>
<script>
import RichTextRenderer from 'contentful-rich-text-vue-renderer'
import { createClient } from '~/plugins/contentful.js'

const client = createClient()

export default {
  components: {
    RichTextRenderer
  },
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
