<template>
  <div>

    <Categories :categories="categories"></Categories>


    <h1>PLP {{params.category}}</h1>



    Facets and Filters
      <ul>
          <li v-if="!facets.length">No item found</li>
          <li v-for="edge in facets">
            <ul>
              <li v-for="value in edge">
                <a v-on:click="addFacet({ type: 'fat', value:'10-12'})">{{edge}}</a>
              </li>
            </ul>
          </li>
      </ul>      

      <ul>
        <li v-for="product in products">
          <!--span v-if="product.fields.categories[0].fields.slug == category.fields.slug"-->          
             <div v-if="product.fields.show">
               <nuxt-link :to="{ name: 'category-path', params: { path: product.fields.path }}">            
                  <h3>{{product.fields.productName}}</h3>
                  <img :src="product.fields.image[0].fields.file.url" />
                </nuxt-link>
              </div>

        <!--/span-->
        </li>
      </ul>

  </div>
</template>


<script>
import {createClient} from '~/plugins/contentful.js'
import Navigation from '~/components/navigation.vue'
import Categories from '~/components/categories.vue'
import Vue from 'vue'

const client = createClient()

export default {
  asyncData ({ env, params }) {
    return Promise.all([
      client.getEntries({
        'content_type': 'category'
      }),
      client.getEntries({
        'content_type': 'product',
        'fields.categories.sys.id': env[params.category],
        include: 10,
        resolveLinks: true
      })
    ]).then(([entries, products]) => {
      for (var f = 0; f < products.items.length; f++) {
        Vue.set(products.items[f].fields, 'show', true)
      }
      return {
        categories: entries.items,
        products: products.items,
        params: params,
        env: env,
        facets: []
      }
    })
    .catch(console.error)
  },
  components: {
    Navigation,
    Categories
  },
  mounted () {
    // fat
    var fatSet = new Set()
    var phSet = new Set()
    for (var y = 0; y < this.products.length; y++) {
      fatSet.add(this.products[y].fields.fat)
      phSet.add(this.products[y].fields.ph)
    }
    this.facets.push(fatSet)
    this.facets.push(phSet)
  },
  methods: {
    addFacet: function (value) {
      console.log('add facet:', value)
      for (var f = 0; f < this.products.length; f++) {
        if (this.products[f].fields.fat !== value.value) {
          Vue.set(this.products[f].fields, 'show', false)
        }
        console.log(this.products[f].fields.show)
      }
      // this.facetsSelected.push(value)
    }
  }
}
</script>
