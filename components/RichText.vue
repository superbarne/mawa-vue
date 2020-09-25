<template>
  <RichTextRenderer :document="content" :node-renderers="renderNodes()" />
</template>
<script>
import { BLOCKS, INLINES } from '@contentful/rich-text-types'
import RichTextRenderer from 'contentful-rich-text-vue-renderer'
import ArticleVideoYoutube from '@/components/ArticleVideoYoutube/ArticleVideoYoutube.vue'

export default {
  components: {
    RichTextRenderer
  },
  props: {
    content: {
      type: Object,
      required: true
    }
  },
  methods: {
    renderNodes () {
      return {
        [BLOCKS.PARAGRAPH]: (node, key, h, next) => {
          return h('b', { key }, next(node.content, key, h, next))
        },
        [INLINES.HYPERLINK]: (node, key, h, next) => {
          if ((node.data.uri).includes('youtube.com/embed')) {
            return h(ArticleVideoYoutube, { key, attrs: { uri: node.data.uri } }, next(node.content, key, h, next))
            // return <YoutubeVideo uri={node.data.uri}></YoutubeVideo>
            // return <><iframe title="Unique Title 002" src={node.data.uri} allow="accelerometer; encrypted-media; gyroscope; picture-in-picture" frameBorder="0" allowFullScreen></iframe></>
          }
        }
      }
    }
  }
}
</script>
