<template>
  <b-container>
    <ArticleSlider :slider-posts="sliderPosts" />
    <b-row>
      <b-col cols="12" md="8">
        <div class="main">
          <ArticleTeaser v-for="post in posts" :key="post.sys.id" :post="post" />
          <infinite-loading @infinite="infiniteHandler" />
        </div>
      </b-col>
      <b-col cols="12" md="4">
        <div class="sidebar">
          <a class="white-box" href="https://www.facebook.com/groups/MoppedAnWeltAus/" title="Mopped an Welt aus - Facebook Gruppe" target="_blank">
            <img src="https://s3.eu-central-1.amazonaws.com/mawa.news/MaWa-Gruppe-Add-XS.png" style="width: 100%">
          </a>
          <div class="white-box">
            <div class="responsive-embed responsive-embed__16by9">
              <iframe
                src="https://www.youtube.com/embed/Zu7fhFgokrw"
                frameborder="0"
                allowfullscreen
              />
            </div>
          </div>
          <div class="white-box">
            <div class="responsive-embed responsive-embed__16by9">
              <iframe
                src="https://www.youtube.com/embed/KJRmMKONL_E"
                frameborder="0"
                allowfullscreen
              />
            </div>
          </div>
          <a class="white-box" href="http://www.motea.com/" title="Motea Online Shop" target="_blank">
            <img src="https://s3.eu-central-1.amazonaws.com/mawa.news/motea-logo.jpg" style="width: 100%">
          </a>
          <a class="white-box" href="https://www.dmd.eu/de/" title="DMD Website" target="_blank">
            <img src="https://s3.eu-central-1.amazonaws.com/mawa.news/dmd-logo.png" style="width: 100%">
          </a>
          <a class="white-box" href="https://partseurope.eu/cms/de/" title="Parts Europe Website" target="_blank">
            <img src="https://s3.eu-central-1.amazonaws.com/mawa.news/parts-europe-logo.jpg" style="width: 100%">
          </a>
          <Footer />
        </div>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import { createClient } from '~/plugins/contentful.js'
const client = createClient()
const limit = 5
export default {
  async asyncData ({ env }) {
    const { items: posts } = await client.getEntries({
      content_type: 'post',
      limit,
      order: '-fields.createdAt'
    })

    const sliderCatagoryId = '563e3302f6b2ab1d1a18938c'
    const { items: sliderPosts } = await client.getEntries({
      content_type: 'post',
      'fields.categories.sys.id': sliderCatagoryId
    })

    return {
      posts,
      sliderPosts
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
        order: '-fields.createdAt'
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
