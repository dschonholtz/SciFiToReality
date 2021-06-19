<template>
  <div>
    <input
      v-model="searchQuery"
      type="Search"
      autocomplete="off"
      placeholder="Search"
      class="search"
    />
    <ul v-if="articles.length" class="search--ul">
      <li v-for="article of articles" :key="article.slug">
        <NuxtLink 
          :to="{ name: 'blog-slug', params: { slug: article.slug } }"
          class="search--link">
          {{ article.title }}
        </NuxtLink>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        searchQuery: '',
        articles: [],
      }
    },
    watch: {
      async searchQuery(searchQuery) {
        if (!searchQuery) {
          this.articles = []
          return
        }
        this.articles = await this.$content('articles')
          .limit(6)
          .search(searchQuery)
          .fetch()
      }
    }
  }
</script>

<style scoped lang="scss">

  .search {
    border-radius: 16px;
    height: 2rem;
    width: 11rem;
    margin-bottom: .5rem;
    margin-top: 1rem;
    margin-left: 0;
    margin-right: .75rem;
    border:1px solid $color-grey-dark-2;

    transition: all .45s;

    &:focus {
      outline: none !important;
      border:1px solid $color-grey-light-2;
      box-shadow: 0 0 10px $color-grey-dark-2;
      width: 13rem;
    }
  
      &--wrapper {
        max-width: 12rem;
        height: 2.5rem;
      }

    &--ul {
      list-style: none;
      padding: 0;
      position: absolute;
      width: auto;
      max-width: 13rem;
      z-index: 10;
      overflow: hidden;
      background-color: white;
      flex: 1 1 0%;
     // top: 10rem;
      border-radius: 0.375rem;
      border: 2px solid $color-grey-light-2;
      // flex-1 top-40 rounded-md border border-gray-30
    }

    &--link {
      //px-4 py-2 items-center leading-5
      color: $color-primary;
      transition: ease-in-out .15s;
      display: flex;
      line-height: 1.25rem;
      padding: 2px 4px;
      margin: .25rem .5rem;
      text-decoration: none;

      &:hover {
        color: black;
      }
    }
  }
  ::placeholder {
    color: $color-grey-dark-2;
  }


</style>