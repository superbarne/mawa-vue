<template>
  <div>
    <b-navbar toggleable="md" type="dark" variant="info" fixed="top">
      <b-container>
        <b-navbar-brand href="#">
          <img src="@/assets/logo.png" alt="">
        </b-navbar-brand>

        <b-navbar-toggle target="nav-collapse" />

        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav>
            <b-nav-item href="#">
              Startseite
            </b-nav-item>
            <b-nav-item href="#">
              Marken
            </b-nav-item>
            <b-nav-item href="#">
              Fahrer
            </b-nav-item>
            <b-nav-item href="#">
              Events
            </b-nav-item>
          </b-navbar-nav>

          <b-navbar-nav class="ml-auto">
            <b-navbar-nav>
              <b-nav-item href="#">
                Facebook
              </b-nav-item>
              <b-nav-item href="#">
                Instagram
              </b-nav-item>
              <b-nav-item href="#">
                YouTube
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
