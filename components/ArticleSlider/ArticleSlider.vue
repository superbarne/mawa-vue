<template>
  <div class="article-slider">
    <VueSlickCarousel v-bind="settings">
      <nuxt-link v-for="post in sliderPostsWithCover" :key="post.sys.id" class="article-slider__item" :to="`/post/${post.fields.slug}`">
        <img :src="post.cover" alt="Image" class="article-slider__item-media">
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
  },
  computed: {
    sliderPostsWithCover () {
      return this.sliderPosts.map((post) => {
        const content = post.fields.content.content
        if (content[0]) {
          const hyperlink = content[0].content.find(item => item.nodeType === 'hyperlink')
          if (hyperlink) {
            if (hyperlink.data.uri.includes('s3.eu-central')) {
              post.cover = hyperlink.data.uri
            }
          }
        }
        return post
      })
    }
  }
}
</script>
