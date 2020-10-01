<template>
  <div class="container prose">
    <div>
      <!-- {{ document.mi_titulo[0].text }} -->
      {{ $prismic.asText(document.mi_titulo) }}
      <img :src="image" alt="" />
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $prismic, error }) {
    try {
      const document = (await $prismic.api.getSingle('blog_post')).data
      console.log(document.img_test.url)
      console.log(document)
      return {
        document,
        image: document.img_test[0].url,
      }
    } catch (e) {
      error({ statusCode: 404, message: 'Page not found' })
    }
  },
  created() {
    console.log(this.image)
  },
}
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
@apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
</style>
