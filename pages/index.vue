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
  async asyncData () {
    const context = await require.context('~/content/blog', true, /\.md$/)
    const posts = context.keys().map((key) => context(key))
    return {
      posts: posts
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
