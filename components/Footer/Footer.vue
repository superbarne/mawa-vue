<template>
  <footer class="footer">
    <!-- <img src="https://via.placeholder.com/1080x400" alt="Full Logo"> -->
    <p>Mopped an, Welt aus!!! © {{ year }}</p>
    <ul>
      <li>
        <a href="/" class="footer__item">Über uns</a>
      </li>
      <li>
        <a href="/impressum" class="footer__item">Impressum</a>
      </li>
      <li>
        <a href="/datenschutz" class="footer__item">Datenschutz</a>
      </li>
    </ul>
  </footer>
</template>

<style lang="scss">
  @import "./Footer.scss";
</style>

<script>
export default {
  data () {
    return {
      year: new Date().getFullYear()
    }
  }
}
</script>
