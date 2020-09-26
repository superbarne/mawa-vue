<template>
  <div>
    <b-navbar toggleable="md" type="dark" fixed="top">
      <b-container>
        <b-navbar-brand to="/">
          <img src="@/assets/logo.png" alt="Logo">
        </b-navbar-brand>

        <b-navbar-toggle target="nav-collapse" />

        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav>
            <b-nav-item to="/">
              Startseite
            </b-nav-item>
            <b-nav-item to="/profile/marken/">
              Marken
            </b-nav-item>
            <b-nav-item to="/profile/fahrer/">
              Fahrer
            </b-nav-item>
            <b-nav-item to="/profile/events/">
              Events
            </b-nav-item>
          </b-navbar-nav>

          <b-navbar-nav class="ml-auto">
            <b-navbar-nav>
              <b-nav-item href="https://www.facebook.com/MoppedAnWeltAus" target="_blank">
                <i class="fab fa-facebook-f" />
              </b-nav-item>
              <b-nav-item href="https://www.instagram.com/moppedanweltaus" target="_blank">
                <i class="fab fa-instagram" />
              </b-nav-item>
              <b-nav-item href="https://www.youtube.com/user/MoppedAnWeltAus" target="_blank">
                <i class="fab fa-youtube" />
              </b-nav-item>
              <b-nav-item href="https://www.twitch.tv/MoppedAnWeltAus" target="_blank">
                <i class="fab fa-twitch" />
              </b-nav-item>
            </b-navbar-nav>
          </b-navbar-nav>
        </b-collapse>
      </b-container>
    </b-navbar>
  </div>
</template>

<style lang="scss">
  @import "./Header.scss";
</style>
