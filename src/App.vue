<template>
  <!-- Don't drop "q-app" class -->
  <div id="q-app">
    <q-layout>
      <div slot="header" class="toolbar">
        <!-- opens drawer using its ref -->
        <button @click="$refs.drawer.open()">
          <i>menu</i>
        </button>

        <q-drawer ref="drawer" swipe-only>
          <div class="list no-border platform-delimiter">
            <div class="toolbar primary">
              <button @click="$refs.drawer.close()">
                <i>close</i>
              </button>
            </div>
            <q-drawer-link v-for="item in menu" 
              :icon="item.icon" 
              :to="item.link" 
              class="text-tertiary">
              {{item.text}}
            </q-drawer-link>
          </div>
        </q-drawer>

        <q-toolbar-title :padding="1">
          {{title}}
        </q-toolbar-title>
        <button>
          <i>more_vert</i>
        </button>
      </div>


      <router-view></router-view>

    </q-layout>
  </div>
</template>

<script>
/*
 * Root component
 */
export default {
  data () {
    return {
      moveX: 0,
      moveY: 0,
      rotateY: 0,
      rotateX: 0,
      title: 'MyBiz',
      menu: [
        {text: 'Home', icon: 'home', link: '/'},
        {text: 'Proposals', icon: 'subject', link: '/proposals'},
        {text: 'Settings', icon: 'settings', link: '/settings'}
      ]
    }
  }
}
</script>

<style>
</style>
