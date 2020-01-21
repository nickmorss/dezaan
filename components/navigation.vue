<template>
  <nav role="navigation" class="top-nav">
    
  <ul class="menu">
    <li><a href="/products" class="">Products</a></li>
    <li><a href="/recipes" class="">Recipes</a></li>
  </ul>

    <!--ul class="menu">
      <li v-if="!/\/.*?\/.*/.test(route.path)" v-for="route in this.$router.options.routes">
        <nuxt-link :to="{ name: route.name }">{{ route.name.charAt(0).toUpperCase() + route.name.slice(1) }}</nuxt-link>
      </li>
    </ul-->
  </nav>
</template>

<style>

  .top-nav {
    width: 100%;
    display: inline-block;
    text-align: right;
    padding: 0 20px 20px 0;
    /* top: -65px;*/
    position: relative;
  }

  .menu {
    display: inline-block;
  }

  .menu li {
    display: inline-block;
    margin-left: 1em;
  }

  .menu a:link,
  .menu a:visited {
    color: #ffffff;
    text-decoration: none;
  }

</style>
