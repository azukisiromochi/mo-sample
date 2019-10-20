<template>
  <div class="container">
    <div>
      <logo />
      <h1 class="title">
        mo-sample
      </h1>
      <h2 ref="h2" class="subtitle" @click="bang">
        My rad Nuxt.js project
      </h2>
      <div class="links">
        <a href="https://nuxtjs.org/" target="_blank" class="button--green">
          Documentation
        </a>
        <a
          href="https://github.com/nuxt/nuxt.js"
          target="_blank"
          class="button--grey"
        >
          GitHub
        </a>
      </div>
    </div>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
import vuemo from '~/plugins/vue-mo'

export default {
  components: {
    Logo
  },
  data() {
    return {
      burst: undefined
    }
  },
  mounted() {
    this.burst = vuemo.burst({
      radius: { 25: 75 },
      count: 10,

      duration: 2000,
      onComplete() {
        console.log('completed')
      },
      children: {
        // property map - maps over children with mod function
        shape: ['circle', 'polygon'],
        // property map - maps over children with mod function
        fill: ['#333', 'magenta', 'purple'],
        angle: { 0: 180 },
        // rand string - generates random value for every child rand( min, max )
        degreeShift: 'rand(-360, 360)',
        // stagger string( start, step ) for every child
        delay: 'stagger(0, 25)'
      }
    })
  },
  methods: {
    bang(e) {
      const x = e.pageX - this.$refs.h2.offsetLeft
      const y = e.pageY - this.$refs.h2.offsetTop
      this.burst.tune({ x, y }).replay()
    }
  }
}
</script>

<style>
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
