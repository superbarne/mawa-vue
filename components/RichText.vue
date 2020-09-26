<template>
  <div>
    <RichTextRenderer :document="content" :node-renderers="renderNodes()" />
  </div>
</template>
<script>
import { INLINES } from '@contentful/rich-text-types'
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
        // [BLOCKS.PARAGRAPH]: (node, key, h, next) => {
        //   return h('b', { key }, next(node.content, key, h, next))
        // },
        [INLINES.HYPERLINK]: (node, key, h, next) => {
          if ((node.data.uri).includes('youtube.com/embed')) { return h(ArticleVideoYoutube, { key, attrs: { uri: node.data.uri } }, next(node.content, key, h, next)) }
          if ((node.data.uri).includes('s3.eu-central')) {
            return h('img', { key, attrs: { src: node.data.uri, width: '100%' } }, next(node.content, key, h, next))
          }
          return h('a', { key }, next(node.content, key, h, next))
        }
      }
    }
  }
}
</script>
