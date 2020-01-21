<template>
	<nav>
      <ul class="items-list wrapper">
        <li class="item" v-for="product in products">
          <nuxt-link :to="{ name: 'categories-slug', params: { slug: category.fields.slug, id: category.sys.id  }}">{{category.fields.title}}</nuxt-link>
      	</li>
      </ul>
	</nav>
</template>

<script>
export default {
  props: ['categories']
}
</script>
