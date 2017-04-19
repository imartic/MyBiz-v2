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

<style>
</style>
