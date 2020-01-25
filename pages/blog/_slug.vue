<template>
  <div>
    <span v-for="(tag, index) in tags" :key="index">

      <nuxt-link :to="'/tag/' + tag">
        {{ tag }}
      </nuxt-link>
    </span>
    <div v-html="html"></div>
  </div>
</template>

<script>
  export default {
    async asyncData ({ params }) {
      try {
        const post = await import(`~/content/blog/${params.slug}.md`)
        return {
          attributes: post.attributes,
          html: post.html,
          tags: post.attributes.tags
        }
      } catch (error) {
        return false
      }
    },
  }
</script>

<style scoped>

</style>
