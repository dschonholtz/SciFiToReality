<template>
  <div class="author-container">
    <NuxtLink :to="`/blog/author/${author.name}`" class="author-link">
      <img :src="require(`~/assets/img/${author.image}`)" :alt="author.alt" class="image-preview"/>
      <div>
        <h4 class="author-header">Author</h4>
        <div class="author-text">
          <p>{{ author.name }}</p>
          <p>{{ author.bio }}</p>
        </div>
      </div>
    </NuxtLink>
  </div>
</template>

<script>
  export default {
    props: {
      author: {
        type: Object,
        required: true
      }
    }
  }
</script>

<style scoped lang='scss'>
  .image-preview {
    display: block;
    max-height:8rem;
    width: auto;
    height: auto;
    border-radius: 50%;
    border-style: solid;
    border-width: 5px;
    border-color: $logo-green;
    position: relative;

    &:before {
      position: absolute;
      z-index: -1;
      border: 6px solid black;
    }
  }

  .author-link {
    text-decoration: none;
    color: $color-grey-dark-3;
    display: inline-flex;
    flex-direction: row;
  }

  .author-header {
    margin-left: 0;
    margin: .25rem;
  }

  .author-text {
    margin: 1rem;
  }

  .author-container {
    padding-top: 3rem;
    padding-bottom: 3rem;
    padding-left: 1rem;
    padding-right: 1rem;
    max-width: $default-content-width - 10rem;
    margin-left: auto;
    margin-right: auto;
  }

</style>