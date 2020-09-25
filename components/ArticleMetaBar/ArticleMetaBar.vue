<template>
  <div class="article-meta">
    <ul>
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
  </div>
</template>

<style lang="scss">
  @import "./ArticleMetaBar.scss";
</style>
