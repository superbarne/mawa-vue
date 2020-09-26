<template>
  <b-container>
    <ProfileDetail :profile="profile" :posts="posts" @posts-load-more="infiniteHandler" />
  </b-container>
</template>

<script>
import { createClient } from '~/plugins/contentful.js'
const client = createClient()
const limit = 3

export default {
  async asyncData ({ env, params: { slug } }) {
    const { items: [profile] } = await client.getEntries({
      content_type: 'profile',
      'fields.slug[in]': slug
    })
    const { items: posts } = await client.getEntries({
      content_type: 'post',
      limit,
      order: '-sys.createdAt',
      'fields.profiles.sys.id': profile.sys.id
    })

    return {
      posts,
      profile
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
        'fields.profiles.sys.id': this.profile.sys.id
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
