<template>
  <article class="article-detail">
    <img src="https://via.placeholder.com/600x400" alt="Image" class="article-detail__media">
    <header class="article-detail__header">
      <h1 class="article-detail__header-title">
        {title} Detail - Headline 1
      </h1>
      <ArticleMetaBar class="article-detail__header-meta" />
    </header>
    <section class="article-detail__body">
      <h2>Body - Headline 2</h2>
      <p> Lorem ipsum dolor sit, amet consectetur adipisicing elit. Voluptatem sequi eaque, ad harum autem vitae, eligendi molestias obcaecati tempore fugit alias asperiores ipsa ab necessitatibus sunt officiis id illo itaque?</p>
    </section>
    <section class="article-detail__footer">
      <h2>Footer - Headline 2</h2>
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Maxime saepe ex eveniet sint. Pariatur qui modi blanditiis id culpa repudiandae expedita cupiditate aspernatur totam? In corporis architecto ut molestiae aliquam!</p>
    </section>
  </article>
</template>

<style lang="scss">
  @import "./ArticleDetail.scss";
</style>
