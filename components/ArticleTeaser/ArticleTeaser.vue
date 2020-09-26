<template>
  <article class="article-teaser">
    <header class="article-teaser__header">
      <router-link :to="`/post/${post.fields.slug}`">
        <h2 class="article-teaser__header-title">
          {{ post.fields.title }}
        </h2>
      </router-link>
      </h2>
      <ArticleMetaBar class="article-teaser__header-meta" :categories="post.fields.categories" :created-at="post.fields.createdAt" />
    </header>
    <section class="article-teaser__body">
      <RichText :content="content" />
    </section>
  </article>
</template>

<style lang="scss">
@import './ArticleTeaser.scss';
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
    content () {
      return {
        ...this.post.fields.content,
        content: [this.post.fields.content.content[0]]
      }
    }
  }
}
</script>
