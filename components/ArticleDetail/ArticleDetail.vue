<template>
  <article class="article-detail">
    <img v-if="headerImage" :src="headerImage" alt="Image" class="article-detail__media">
    <ArticleVideoYoutube v-if="headerYoutube" :uri="headerYoutube" class="article-detail__media" />
    <header class="article-detail__header">
      <h1 class="article-detail__header-title">
        {{ post.fields.title }}
      </h1>
      <ArticleMetaBar class="article-teaser__header-meta" :profiles="post.fields.profiles" :categories="post.fields.categories" :created-at="post.fields.createdAt" />
    </header>
    <section class="article-detail__body">
      <RichText :content="content" />
    </section>
    <!--section class="article-detail__footer">
      <h2>Footer - Headline 2</h2>
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Maxime saepe ex eveniet sint. Pariatur qui modi blanditiis id culpa repudiandae expedita cupiditate aspernatur totam? In corporis architecto ut molestiae aliquam!</p>
    </section-->
  </article>
</template>

<style lang="scss">
  @import "./ArticleDetail.scss";
</style>

<script>
export default {
  props: {
    post: {
      type: Object,
      required: true
    }
  },
  computed: {
    headerImage () {
      const content = this.post.fields.content.content
      if (!content[0]) { return null }
      const hyperlink = content[0].content.find(item => item.nodeType === 'hyperlink')
      if (hyperlink) {
        if (hyperlink.data.uri.includes('s3.eu-central')) {
          return hyperlink.data.uri
        }
      }
      return null
    },
    headerYoutube () {
      const content = this.post.fields.content.content
      if (!content[0]) { return null }
      const hyperlink = content[0].content.find(item => item.nodeType === 'hyperlink')
      if (hyperlink) {
        if (hyperlink.data.uri.includes('youtube.com/embed')) {
          return hyperlink.data.uri
        }
      }
      return null
    },
    content () {
      const content = [...this.post.fields.content.content]
      if (content[0]) {
        const hyperlink = content[0].content.find(item => item.nodeType === 'hyperlink')
        if (hyperlink) {
          if (hyperlink.data.uri.includes('s3.eu-central') || hyperlink.data.uri.includes('youtube.com/embed')) {
            content.shift()
          }
        }
      }
      return {
        ...this.post.fields.content,
        content
      }
    }
  }
}
</script>
