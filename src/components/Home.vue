<template>
  <div class="home-page window-height window-width bg-light column items-center">
    <div class="home-code bg-primary flex items-center justify-center">
      
      <div class="bg-logo logo-container non-selectable no-pointer-events">
        <div class="logo" :style="position">
          <img src="~assets/quasar-logo.png">
          <p class="home-title text-center text-white">MyBiz</p>
        </div>
      </div>

    </div>
    <div>
        <div class="card home-card bg-white">
          <div class="list item-delimiter">
            <q-collapsible opened group="home-group" label="Sign in">
              <div class="home-form">
                <div class="row wrap small-gutter" style="margin-bottom:20px">
                  <div class="auto row home-form-input">
                    <span class="label text-primary"><i>person_outline</i></span>
                    <input class="auto" v-model="username" placeholder="Username">
                  </div>
                  <div class="auto row home-form-input">
                    <span class="label text-primary"><i>lock_outline</i></span>
                    <input class="auto" v-model="password" placeholder="Password">
                  </div>
                </div>
                <label class="remember-me">
                  <q-checkbox v-model="rmChecked"></q-checkbox>
                  Remember me
                </label>
                <button class="primary clear full-width" @click="signIn()">
                  Sign in
                </button>
              </div>
            </q-collapsible>
            <q-collapsible group="home-group" label="Sign up">
              <div>
                <div class="home-form">
                  <div class="row wrap small-gutter" style="margin-bottom:20px">
                    <div class="auto row home-form-input">
                      <span class="label text-primary"><i>mail_outline</i></span>
                      <input class="auto" v-model="mail" placeholder="E-mail">
                    </div>
                    <div class="auto row home-form-input">
                      <span class="label text-primary"><i>person_outline</i></span>
                      <input class="auto" v-model="username_new" placeholder="Username">
                    </div>
                    <div class="auto row home-form-input">
                      <span class="label text-primary"><i>lock_outline</i></span>
                      <input class="auto" v-model="password_new" placeholder="Password">
                    </div>
                    <div class="auto row home-form-input">
                      <span class="label text-primary"><i>lock_outline</i></span>
                      <input class="auto" v-model="confirmPassword" placeholder="Confirm Password">
                    </div>
                  </div>
                  <button class="primary clear full-width" @click="signIn()">
                    Create account
                  </button>
                </div>
              </div>
            </q-collapsible>
          </div>
      </div>
    </div>
  </div>
</template>

<script>
var moveForce = 30
var rotateForce = 40

import { Utils } from 'quasar'

export default {
  data () {
    return {
      moveX: 0,
      moveY: 0,
      rotateY: 0,
      rotateX: 0,
      username: '',
      password: '',
      rmChecked: false,
      mail: '',
      username_new: '',
      password_new: '',
      confirmPassword: ''
    }
  },
  computed: {
    position () {
      let transform = `rotateX(${this.rotateX}deg) rotateY(${this.rotateY}deg)`
      return {
        top: this.moveY + 'px',
        left: this.moveX + 'px',
        '-webkit-transform': transform,
        '-ms-transform': transform,
        transform
      }
    }
  },
  methods: {
    move (event) {
      const {width, height} = Utils.dom.viewport()
      const {top, left} = Utils.event.position(event)
      const halfH = height / 2
      const halfW = width / 2

      this.moveX = (left - halfW) / halfW * -moveForce
      this.moveY = (top - halfH) / halfH * -moveForce
      this.rotateY = (left / width * rotateForce * 2) - rotateForce
      this.rotateX = -((top / height * rotateForce * 2) - rotateForce)
    }
  },
  mounted () {
    this.$nextTick(() => {
      document.addEventListener('mousemove', this.move)
      document.addEventListener('touchmove', this.move)
    })
  },
  beforeDestroy () {
    document.removeEventListener('mousemove', this.move)
    document.removeEventListener('touchmove', this.move)
  }
}
</script>

<style lang="stylus">
.bg-logo
  opacity 1
.logo-container
  width 192px
  height 268px
  perspective 800px
  position absolute
  top 27%
  left 50%
  transform translateX(-50%) translateY(-50%)
.logo
  position absolute
  transform-style preserve-3d
.home-title
  font-size 30px
  font-weight 600
  margin-top 10px

.home-page
  .home-code
    height 50vh
    width 100%
    padding-top 15vh
    font-size 90px
    color rgba(255, 255, 255, .5)
    overflow hidden
  .home-card
    margin-top -25px
    width 90vw
    max-width 600px
    padding 0px

.sign-in-btn:hover, .sign-in-btn:active, .sign-in-btn:focus
  background:transparent !important
  text-decoration:underline

.q-collapsible > .item > .item-content > div
  overflow:unset !important
  font-weight 600

.home-form i
  font-size 24px

.home-form button
  margin-top 20px

.home-form input
  width auto

.home-form-input
  padding-left 0 !important
  margin-right 10px
  margin-bottom 10px
  margin-top 5px

.remember-me
  padding-left 5px

.home-card .q-collapsible-sub-item
  padding-left 8px
  padding-right 8px
</style>
