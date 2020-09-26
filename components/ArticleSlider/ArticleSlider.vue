<template>
  <div class="article-slider">
    <VueSlickCarousel v-bind="settings">
      <div class="article-slider__item">
        <img src="https://via.placeholder.com/1080x400" alt="Image" class="article-slider__item-media">
        <div class="article-slider__item-caption">
          <h3 class="article-slider__item-title">
            Headline 3
          </h3>
        </div>
      </div>
      <div class="article-slider__item">
        <img src="https://via.placeholder.com/1080x400" alt="Image" class="article-slider__item-media">
        <div class="article-slider__item-caption">
          <h3 class="article-slider__item-title">
            Headline 3
          </h3>
        </div>
      </div>
      <div class="article-slider__item">
        <img src="https://via.placeholder.com/1080x400" alt="Image" class="article-slider__item-media">
        <div class="article-slider__item-caption">
          <h3 class="article-slider__item-title">
            Headline 3
          </h3>
        </div>
      </div>
    </VueSlickCarousel>
  </div>
</template>

<style lang="scss">
  @import "./ArticleSlider.scss";
  @import 'vue-slick-carousel/dist/vue-slick-carousel.css';
</style>

<script>
import VueSlickCarousel from 'vue-slick-carousel'

export default {
  components: { VueSlickCarousel },
  data () {
    return {
      settings: {
        infinite: true,
        slidesToShow: 1,
        slidesToScroll: 1,
        responsive: [
          {
            breakpoint: 992,
            settings: {
              dots: false
            }
          },
          {
            breakpoint: 768,
            settings: {
              arrows: true,
              dots: false
            }
          },
          {
            breakpoint: 576,
            settings: {
              arrows: false,
              dots: true
            }
          }
        ]
      }
    }
  }
}
</script>
