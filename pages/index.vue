<template>
  <section class="container">
    <div>
      <logo/>
      <h1 class="title">
        example-vue-masonry-ssr
      </h1>
      <h2 class="subtitle">
        An example template for using vue-masonry with nuxt ssr
      </h2>
      <div class="links">
        <a href="https://nuxtjs.org/" target="_blank" class="button--green">Documentation</a>
        <a href="https://github.com/nuxt/nuxt.js" target="_blank" class="button--grey">GitHub</a>
      </div>

      <no-ssr>
        <div v-masonry transition-duration="3s" item-selector=".item" class="masonry-container">
          <div v-masonry-tile class="item" :key="index" v-for="(item, index) in blocks">
            <p>{{item.title}} - {{index}}</p>
          </div>
        </div>
      </no-ssr>
    </div>
  </section>
</template>

<script>
import Logo from '~/components/Logo.vue'

import NoSSR from 'vue-no-ssr'
export default {
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      blocks: [
        {
          title: 'nice block'
        },
        {
          title: 'another shiny block'
        },
        {
          title: 'the last block'
        }
      ]
    }
  },
  mounted () {
    if (typeof this.$redrawVueMasonry === 'function') {
      this.$redrawVueMasonry()
    }
  },
  components: {
    Logo,
    'no-ssr': NoSSR
  }
}
</script>

<style>
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
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

.item {
  border: 1px solid #ac0;
  width: 200px;
}

.masonry-container {
  width: 55%;
  margin: 0 auto;
}

</style>
