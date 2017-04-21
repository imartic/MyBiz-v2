<template>
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
                class="text-dark">
                {{item.text}}
            </q-drawer-link>
            </div>
        </q-drawer>

        <q-toolbar-title :padding="1">
            {{title}}
        </q-toolbar-title>

        <button @click="$refs.userDrawer.open()">
            <i>person</i>
        </button>

        <q-drawer ref="userDrawer" swipe-only right-side dark :backdrop-opacity="0.2">
        <div class="list no-border platform-delimiter">
        <div class="toolbar primary">
            <button @click="$refs.userDrawer.close()">
                <i>close</i>
            </button>
        </div>
        <q-drawer-link v-for="item in userMenu" 
            :icon="item.icon" 
            :to="item.link" 
            class="text-dark">
            {{item.text}}
        </q-drawer-link>
        </div>
    </q-drawer>
    </div>

</q-layout>
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
      ],
      userMenu: [
        {text: 'Your companies', icon: 'business', link: '/companies'},
        {text: 'Account settings', icon: 'settings', link: '/account'},
        {text: 'Sign out', icon: 'power_settings_new', link: '/signin'}
      ]
    }
  }
}
</script>

<style lang="stylus">

</style>
