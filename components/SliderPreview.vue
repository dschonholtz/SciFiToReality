<template>
    <NuxtLink :to="{ name: 'blog-slug', params: { slug: article.slug } }">
        <img :src="require(`~/assets/img/${article.img}`)" alt="" uk-cover>
        <div class="uk-overlay uk-overlay-default uk-position-bottom-right uk-position-small">
            <h3 class="uk-margin-remove">{{ article.title }}</h3>
        </div>
    </NuxtLink>
</template>

<script>
  export default {
    props: ['article'],
  }
</script>

<style scoped lang="scss">

</style>
