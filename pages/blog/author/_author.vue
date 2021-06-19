<template>
  <div class="container">
      <Author :author="articles[0].author"/>
      <div class="more-margin-container">
        <div v-for="article in articles" :key="article.slug">
          <blog-preview :article="article"></blog-preview>
        </div>
      </div>
  </div>
</template>

<script>
  export default {
    async asyncData({ $content, params }) {
      const articles = await $content('articles', params.slug)
        .where({
          'author.name': {
            $regex: [params.author, 'i']
          }
        })
        .without('body')
        .sortBy('createdAt', 'asc')
        .fetch()

      return {
        articles
      }
    },
    methods: {
      formatDate(date) {
        const options = { year: 'numeric', month: 'long', day: 'numeric' }
        return new Date(date).toLocaleDateString('en', options)
      }
    }
  }
</script>

<style scoped lang="scss">

  .more-margin-container {
    max-width: $default-content-width;
    margin-left: auto;
    margin-right: auto;
  }

</style>