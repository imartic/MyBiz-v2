<template>
  <div class="home-page window-height window-width bg-light column items-center">
    <div class="home-code bg-primary flex items-center justify-center">
      
      <div class="bg-logo logo-container non-selectable no-pointer-events">
        <div class="logo" :style="position">
          <img src="~assets/quasar-logo.png" height="150px" width="150px">
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
                    <input id="username" class="auto" v-model="username" placeholder="Username">
                  </div>
                  <div class="auto row home-form-input">
                    <span class="label text-primary"><i>lock_outline</i></span>
                    <input id="password" class="auto" v-model="password" placeholder="Password">
                  </div>
                </div>
                <label class="remember-me">
                  <q-checkbox v-model="rmChecked"></q-checkbox>
                  Remember me
                </label>

                <div v-if="signInError" class='input-error bg-negative'>
                  <span class="close-error" @click="closeError(1)">&times;</span> 
                  {{signInErrorMsg}}
                </div>

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
                      <input id="mail" class="auto" v-model="mail" placeholder="E-mail">
                    </div>
                    <div class="auto row home-form-input">
                      <span class="label text-primary"><i>person_outline</i></span>
                      <input id="username_new" class="auto" v-model="username_new" placeholder="Username">
                    </div>
                    <div class="auto row home-form-input">
                      <span class="label text-primary"><i>lock_outline</i></span>
                      <input id="password_new" class="auto" v-model="password_new" placeholder="Password">
                    </div>
                    <div class="auto row home-form-input">
                      <span class="label text-primary"><i>lock_outline</i></span>
                      <input id="confirmPassword" class="auto" v-model="confirmPassword" placeholder="Confirm Password">
                    </div>
                  </div>

                  <div v-if="signUpError" class='input-error bg-negative'>
                    <span class="close-error" @click="closeError(2)">&times;</span> 
                    {{signUpErrorMsg}}
                  </div>

                  <button class="primary clear full-width" @click="register()">
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
var moveForce = 15
var rotateForce = 25

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
      confirmPassword: '',
      signInError: false,
      signInErrorMsg: '',
      signUpError: false,
      signUpErrorMsg: ''
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
    },
    signIn () {
      if (this.username.length < 1) { // todo: validation
        this.signInError = true
        this.signInErrorMsg = 'Please enter your username or e-mail address.'
        document.getElementById('username').focus()
        return
      }
      if (this.password.length < 1) { // ...
        this.signInError = true
        this.signInErrorMsg = 'Please enter a password.'
        document.getElementById('password').focus()
        return
      }

      this.closeError(1)

      console.log('SIGNED IN WITH:\n' +
            'Username: ' + this.username + '\n' +
            'Password: ' + this.password + '\n' +
            'Remember me: ' + this.rmChecked)

      this.$router.push('/')
    },
    register () {
      let conf = (this.password_new === this.confirmPassword)
            ? 'Password confirmed!'
            : 'Passwords do not match!'

      if (this.mail.length < 1) { // todo: validation
        this.signUpError = true
        this.signUpErrorMsg = 'Please enter your e-mail address.'
        document.getElementById('mail').focus()
        return
      }
      if (this.username_new.length < 1) {
        this.signUpError = true
        this.signUpErrorMsg = 'Please enter a username.'
        document.getElementById('username_new').focus()
        return
      }
      if (this.password_new.length < 4) {
        this.signUpError = true
        this.signUpErrorMsg = 'Password must contain at least 4 characters.'
        document.getElementById('password_new').focus()
        return
      }
      if (this.password_new !== this.confirmPassword) {
        this.signUpError = true
        this.signUpErrorMsg = 'Passwords do not match.'
        document.getElementById('confirmPassword').focus()
        return
      }

      this.closeError(2)

      console.log('REGISTERED:\n' +
            'E-mail: ' + this.mail + '\n' +
            'Username: ' + this.username_new + '\n' +
            'Password: ' + this.password_new + '\n' +
            conf)
    },
    closeError (no) { // 1 = sign in, 2 = sign up
      if (no === 1) {
        this.signInError = false
        this.signInErrorMsg = ''
      }
      else if (no === 2) {
        this.signUpError = false
        this.signUpErrorMsg = ''
      }
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
  width 150px
  height 150px
  perspective 800px
  position absolute
  top 20%
  left 50%
  transform translateX(-50%) translateY(-50%)
.logo
  position absolute
  transform-style preserve-3d

.home-page
  .home-code
    height 40vh
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

.input-error
    padding 18px
    border-radius 2px
    color white
    font-size 15px
    margin-top:20px
.close-error
    margin-left 15px
    color white
    font-weight bold
    float right
    font-size 22px
    line-height 20px
    cursor pointer
    transition 0.3s
.close-error:hover
    color black
</style>
