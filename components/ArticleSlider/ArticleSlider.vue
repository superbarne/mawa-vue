<template>
  <div class="article-slider">
    <VueSlickCarousel v-bind="settings">
      <nuxt-link v-for="post in sliderPosts" :key="post.sys.id" class="article-slider__item" :to="`/post/${post.fields.slug}`">
        <img src="https://via.placeholder.com/1080x400" alt="Image" class="article-slider__item-media">
        <div class="article-slider__item-caption">
          <h3 class="article-slider__item-title">
            {{ post.fields.title }}
          </h3>
        </div>
      </nuxt-link>
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
  props: {
    sliderPosts: {
      type: Array,
      required: false,
      default: () => []
    }
  },
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
