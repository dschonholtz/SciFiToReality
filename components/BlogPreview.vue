<template>
<NuxtLink :to="{ name: 'blog-slug', params: { slug: article.slug } }">
  <div class="uk-card uk-card-large uk-card-default uk-grid-collapse uk-child-width-1-2@s uk-margin uk-card-hover" uk-grid>
    <div class="uk-card-media-left uk-cover-container">
        <img :src="require(`~/assets/img/${article.img}`)" :alt="article.alt" uk-cover>
        <canvas width="600" height="400"></canvas>
    </div>
    <div>
        <div class="uk-card-body">
            <h4 class="uk-card-title">{{ article.title }}</h4>
        </div>
    </div>
  </div>
</NuxtLink>
</template>

<script>
  export default {
    props: ['article']
  }
</script>

<style scoped lang="scss">
</style>
