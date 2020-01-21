<template>
	<nav>
      <ul class="items-list wrapper">
        <li class="item" v-for="category in categories">
          <nuxt-link :to="{ name: 'category', params: { category: category.fields.slug }}">{{category.fields.title}}</nuxt-link>
      	</li>
      </ul>
	</nav>
</template>

<script>
export default {
  props: ['categories']
}
</script>
