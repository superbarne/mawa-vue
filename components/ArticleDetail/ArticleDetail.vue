<template>
  <article class="article-detail">
    <header>
      <h2 class="title">
        {title} Detail
      </h2>
      <ul class="tags">
        <li>
          <i class="fas fa-clock" />
          <span>
            {new Intl.DateTimeFormat("de-DE", {
            year: "numeric",
            month: "long",
            day: "2-digit"
            }).format(createdAtDate)}
          </span>
        </li>
        <li>
          <i class="fas fa-star" />
          <a href="/">Profile</a>
        </li>
        <li>
          <i class="fas fa-tags" />
          <a href="/">#Tag1</a>
          <a href="/">#Tag2</a>
        </li>
      </ul>
    </header>
    <section class="content">
      <img src="https://via.placeholder.com/600x400" alt="Image" class="media">
      <p> Lorem ipsum dolor sit, amet consectetur adipisicing elit. Voluptatem sequi eaque, ad harum autem vitae, eligendi molestias obcaecati tempore fugit alias asperiores ipsa ab necessitatibus sunt officiis id illo itaque?</p>
    </section>
  </article>
</template>

<style lang="scss">
  @import "./ArticleDetail.scss";
</style>
