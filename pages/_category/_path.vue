<template>
  <div>PDP

  <nuxt-link :to="{ name: 'category', params: { category: params.category }}">Back</nuxt-link>
    

    <h1>{{product.fields.productName}}</h1>    
    <img :src="product.fields.image[0].fields.file.url" />
    <ul>
      <li>{{product.fields.fat}}</li>
      <li>{{product.fields.formats}}</li>
      <li>{{product.fields.sku}}</li>
    </ul>


  </div>
</template>

<script>
import {createClient} from '~/plugins/contentful.js'
import Navigation from '~/components/navigation.vue'

const client = createClient()

export default {
  asyncData ({ env, params }) {
    return Promise.all([
      client.getEntries({
        'content_type': 'product',
        'fields.path': params.path,
        // 'fields.categories.sys.id': env.'CTF_' + params.slug + '_ID',
        include: 10,
        resolveLinks: true
      })
    ]).then(([entries]) => {
      return {
        product: entries.items[0],
        params: params,
        env: env
      }
    })
    .catch(console.error)
  },
  components: {
    Navigation
  }
}
</script>
