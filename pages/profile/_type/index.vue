<template>
  <b-container>
    <pre>{{ profiles }}</pre>
  </b-container>
</template>

<script>
import { createClient } from '~/plugins/contentful.js'
const client = createClient()

export default {
  async asyncData ({ env, params: { type } }) {
    const { items: profiles } = await client.getEntries({
      content_type: 'profile',
      order: 'fields.name',
      'fields.type': type
    })

    return {
      profiles
    }
  }
}
</script>
