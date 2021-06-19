<template>
<div>
  <div class="uk-section uk-section-default uk-padding-remove-vertical">
    <div class="uk-position-relative uk-visible-toggle" tabindex="-1" uk-slideshow="animation: fade; ratio: false; autoplay: true">

      <ul class="uk-slideshow-items uk-grid" uk-height-viewport="offset-top: true; offset-bottom: 50">
          <li v-for="article of articles" :key="article.slug" class="uk-width-1-1">
              <slider-preview :article="article"></slider-preview>
          </li>
      </ul>

        <a class="uk-position-center-left uk-position-small uk-hidden-hover" href="#" uk-slidenav-previous uk-slideshow-item="previous"></a>
        <a class="uk-position-center-right uk-position-small uk-hidden-hover" href="#" uk-slidenav-next uk-slideshow-item="next"></a>

    </div>
  </div>
  
  <div class="uk-section uk-section-default">
    <div class="uk-container uk-container-large">
      <div class="uk-grid-medium uk-child-width-expand@s uk-text-center" uk-scrollspy="cls: uk-animation-fade; target: .uk-card; delay: 400" uk-grid>
        <div v-for="article of articles" :key="article.slug" class="uk-width-1-2">
          <blog-preview :article="article"></blog-preview>
        </div>
      </div>
    </div>
  </div>
</div>
</template>

<script>
import BlogPreview from "~/components/BlogPreview.vue"
import SliderPreview from "~/components/SliderPreview.vue"

  export default {
    components: { BlogPreview, SliderPreview },
    async asyncData({ $content, params }) {
      const articles = await $content('articles', params.slug)
        .only(['title', 'description', 'img', 'slug', 'author'])
        .sortBy('updatedAt', 'desc')
        .fetch()

      return {
        articles
      }
    },
    data() {
      return { 
        window: {
            width: 0,
            height: 0
        }
      }
    },
    computed: {
      slideShowHeight() {
        return "offset-top: true; offset-bottom: " + this.window.height * .5;
      }
    },
    mounted() {
        window.addEventListener('resize', this.handleResize);
        this.handleResize();
    },
    destroyed() {
        window.removeEventListener('resize', this.handleResize);
    },
    methods: {
        handleResize() {
            this.window.width = window.innerWidth;
            this.window.height = window.innerHeight;
        }
    }
  }
</script>

<style lang="scss" scoped>
</style>
