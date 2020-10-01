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
