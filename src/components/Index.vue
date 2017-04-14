<template>
  <q-layout>
    <!--
      Replace following "div" with
      "<router-view class="layout-view">" component
      if using subRoutes
    -->
    <div class="layout-view">
      <div class="bg-logo logo-container non-selectable no-pointer-events">
        <div class="logo" :style="position">
          <img src="~assets/quasar-logo.png">
          <p class="home-title text-center text-primary">MyBiz</p>
        </div>
      </div>

      <div class="layout-padding">
        <h1>Welcome to <b>MyBiz</b>.</h1>
        <br/>
        

        <div class="row small-gutter">
          <div class="auto">
            <div class="card">
              <div class="card-title bg-primary text-white">
                <span>Proposals</span>
              </div>
              <div class="card-media">
                <button class="secondary circular">
                  <i>add</i>
                  <q-tooltip>
                      New proposal
                  </q-tooltip>
                </button>
              </div>
              <div class="card-content card-force-top-padding">
                <br/>
                <table class="q-table home-table loose">
                  <thead>
                    <tr>
                      <th class="text-left" width="65%">Proposal</th>
                      <th class="text-left">Date created</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="proposal in proposals">
                      <td class="text-left">{{proposal.name}}</td>
                      <td class="text-left">{{proposal.date}}</td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </div>
          </div>
          <div class="auto">
            <div class="card">
              <div class="card-title bg-primary text-white">
                <span>Schedule</span>
              </div>
              <div class="card-media">
                <button class="secondary circular">
                  <i>add</i>
                  <q-tooltip>
                      New task
                  </q-tooltip>
                </button>
              </div>
              <div class="card-content card-force-top-padding">
                <br/>
                <table class="q-table home-table loose">
                  <thead>
                    <tr>
                      <th class="text-left" width="65%">Task</th>
                      <th class="text-left">Date</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="item in schedule">
                      <td class="text-left">{{item.name}}</td>
                      <td class="text-left">{{item.date}}</td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </div>
          </div>

        </div>
      </div>
    </div>
  </q-layout>
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
      proposals: [
        { name: 'Proposal One', date: '12.4.2017' },
        { name: 'Proposal Two', date: '22.3.2017' },
        { name: 'Proposal Three', date: '10.2.2017' }
      ],
      schedule: [
        { name: 'Task One', date: '12.4.2017' },
        { name: 'Task Two', date: '22.3.2017' },
        { name: 'Task Three', date: '10.2.2017' }
      ]
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
  opacity 0.3
.logo-container
  width 192px
  height 268px
  perspective 800px
  position absolute
  top 80%
  left 50%
  transform translateX(-50%) translateY(-50%)
.logo
  position absolute
  transform-style preserve-3d
.home-title
  font-size 30px
  font-weight 600
  margin-top 15px
.home-table
  width 100%
</style>
