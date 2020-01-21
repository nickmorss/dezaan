<template>
  <div>

    <h2>The future of cocoa since 1911</h2>

    <p>Lorem ipsizzle da bomb sit amizzle, yippiyo adipiscing elizzle. Nullam sure velizzle, black volutpizzle, mammasay mammasa mamma oo sa things, away fo shizzle, arcu. Pellentesque eget tortor. Sed erizzle. For sure fizzle dolizzle get down get down pot tempizzle shit.</p>

    <section class="body-container">
      <div class="items-bar wrapper">
        <h2>Top Recipes</h2>
      </div>
      <ul class="items-list wrapper">
        <li class="item" v-for="post in posts">
          <article-preview :post="post"></article-preview>
        </li>
      </ul>
    </section>

  </div>
</template>

<script>
import {createClient} from '~/plugins/contentful.js'
import Navigation from '~/components/navigation.vue'
import ArticlePreview from '~/components/article-preview.vue'

const client = createClient()

export default {
  asyncData ({env}) {
    return Promise.all([
      client.getEntries({
        'sys.id': env.CTF_PERSON_ID
      }),
      client.getEntries({
        'content_type': env.CTF_BLOG_POST_TYPE_ID,
        order: '-sys.createdAt'
      }),
      client.getEntries({
        'content_type': 'product',
        order: '-sys.createdAt'
      }),
      client.getEntries({
        'content_type': 'category',
        order: '-sys.createdAt',
        include: '10'
      })
    ]).then(([entries, posts, products, categories]) => {
      return {
        person: entries.items[0],
        posts: posts.items,
        products: products.items,
        categories: categories
      }
    }).catch(console.error)
  },
  components: {
    Navigation,
    ArticlePreview
  }
}
</script>
