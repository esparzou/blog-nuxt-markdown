<template>
  <div class="container">
    <div v-for="post in posts" :key="post.attributes.title">
      <h2>{{ post.attributes.title }}</h2>
      <h3>{{ post.attributes.date }}</h3>
      <p>{{ post.attributes.excerpt }}</p>
      <nuxt-link :to="'/blog/' + post.attributes.path">
        Continuar leyendo
      </nuxt-link>
    </div>
  </div>
</template>

<script>
  export default {
    async asyncData({ params }) {
      const resolve = await require.context('~/content/blog/', true, /\.md$/)
      let imports = resolve.keys().map((key) => resolve(key))
      // filter out page type
      imports = imports.filter((post) => !post.attributes.type)
      imports = imports.filter(
        (post) => post.attributes.tags.filter((tag) => tag === params.slug).length
      )
      console.log(imports)
      return {
        posts: imports
      }
    },
  }
</script>

<style lang="scss" scoped>

</style>
