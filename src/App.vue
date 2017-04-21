<template>
  <!-- Don't drop "q-app" class -->
  <div id="q-app">
    
    <Layout></Layout> <!-- todo: v-if user authenticated -->
    <router-view></router-view>

  </div>
</template>

<script>
import Layout from './components/Layout'

export default {
  data () {
    return {
      title: 'MyBiz'
    }
  },
  components: {
    Layout
  }
}
</script>

<style lang="stylus">
@media (min-width 1200px)
  .layout-padding
    padding-left 150px
    padding-right 150px

@media (min-width 1600px)
  .layout-padding
    padding-left 300px
    padding-right 300px

.layout-padding
    padding-top 2.5rem !important
</style>
