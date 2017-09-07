# example-vue-masonry-ssr

> An example template for using vue-masonry with nuxt ssr

## Build Setup

``` bash
# install dependencies
$ npm install # Or yarn install

# serve with hot reload at localhost:3000
$ npm run dev

# build for production and launch server
$ npm run build
$ npm start

# generate static project
$ npm run generate
```

### NUXT ssr implimentation

The best way to impliment this is to use the [no-ssr plugin](https://github.com/egoist/vue-no-ssr).

1. Create a file in your plugins folder called vue-masonry.js with the following contents:

```
import Vue from 'vue'
import VueMasonryPlugin from 'vue-masonry'

Vue.use(VueMasonryPlugin)
```
2. Add this plugin to your `nuxt.config.js`

```
  plugins: [
    { src: '~/plugins/vue-masonry', ssr: false }
  ]
```

(NB make sure ssr is set to false)

3. Add no-ssr and the markup for your vue-masonry to a component:

HTML:
```
    <no-ssr>
      <div v-masonry transition-duration="3s" item-selector=".item" class="masonry-container">
        <div v-masonry-tile class="item" :key="index" v-for="(item, index) in blocks">
          <p>{{item}} - {{index}}</p>
        </div>
      </div>
    </no-ssr>
```

JS:
```
  import NoSSR from 'vue-no-ssr'

  export default {
    components: {
      'no-ssr': NoSSR
    },
    mounted () {
      if (typeof this.$redrawVueMasonry === 'function') {
        this.$redrawVueMasonry()
      }
    }
  }
```

For detailed explanation on how things work, checkout the [Nuxt.js docs](https://github.com/nuxt/nuxt.js).
