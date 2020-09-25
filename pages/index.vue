<template>
  <div class="container">
    <div>
      <Logo />
      <h1 class="title">
        mawa
      </h1>
      <div class="links">
        <a
          href="https://nuxtjs.org/"
          target="_blank"
          rel="noopener noreferrer"
          class="button--green"
        >
          Documentation
        </a>
        <a
          href="https://github.com/nuxt/nuxt.js"
          target="_blank"
          rel="noopener noreferrer"
          class="button--grey"
        >
          GitHub
        </a>
      </div>
    </div>
    <pre>{{ posts }}</pre>
  </div>
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
