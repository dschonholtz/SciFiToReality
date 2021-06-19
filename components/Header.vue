<template>
<nav class="uk-navbar-container" uk-navbar>
    <div class="nav-overlay uk-navbar-left">
        <NuxtLink class="uk-navbar-item uk-logo" to="/">Daily Progress</NuxtLink>
        <ul class="uk-navbar-nav">
            <li :class="this.aboutActive"><NuxtLink to="/blog/About">About</NuxtLink></li>
            <li :class="this.dailyActive"><NuxtLink to="/daily">Dailies</NuxtLink></li>
        </ul>
    </div>

    <div class="nav-overlay uk-navbar-right">
        <app-search-input/>
    </div>

    <div class="nav-overlay uk-navbar-left uk-flex-1" hidden>

        <div class="uk-navbar-item uk-width-expand">
            <form class="uk-search uk-search-navbar uk-width-1-1">
                <input class="uk-search-input" type="search" placeholder="Search" autofocus>
            </form>
        </div>

        <a class="uk-navbar-toggle" uk-close uk-toggle="target: .nav-overlay; animation: uk-animation-fade" href="#"></a>

    </div>

</nav>

</template>


<script>
  export default {
    data() {
        let about = '';
        let daily = ''; 
        if (this.$nuxt.$route.name.includes('dail')) {
            daily = 'uk-active'; 
        }
        else if (this.$nuxt.$route.name.includes('/blog/About')) {
            about= 'uk-active';
        }
      return {
        aboutActive: about,
        dailyActive: daily,
      }
    },
  }
</script>

<style scoped lang="scss">
</style>