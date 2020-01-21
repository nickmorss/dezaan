<template>
  <div>
      <div class="items-bar wrapper">
        <h2>Category Landing</h2>
      </div>
      <Categories :categories="categories"></Categories>
  </div>
</template>

<script>
import {createClient} from '~/plugins/contentful.js'
import Navigation from '~/components/navigation.vue'
import Categories from '~/components/categories.vue'
import ArticlePreview from '~/components/article-preview.vue'

const client = createClient()

export default {
  asyncData ({env}) {
    return Promise.all([
      client.getEntries({
        'content_type': 'category',
        order: '-sys.createdAt',
        include: '10'
      })
    ]).then(([entries]) => {
      return {
        categories: entries.items
      }
    }).catch(console.error)
  },
  components: {
    Navigation,
    Categories,
    ArticlePreview
  }
}
</script>
