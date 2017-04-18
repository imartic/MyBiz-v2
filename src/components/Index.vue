<template>
  <q-layout>
    <!--
      Replace following "div" with
      "<router-view class="layout-view">" component
      if using subRoutes
    -->
    <div class="layout-view">

      <div class="layout-padding">
        <h1>Welcome to <b>MyBiz</b>.</h1>
        <br/>
        
        <div class="row wrap small-gutter">
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
              <div class="card-actions card-no-top-padding">
                <button class="primary full-width clear small">
                  View all proposals
                </button>
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
              <div class="card-actions card-no-top-padding">
                <button class="primary full-width clear small">
                  View full schedule
                </button>
              </div>
            </div>
          </div>

        </div>
      </div>
    </div>
  </q-layout>
</template>

<script>
export default {
  data () {
    return {
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
  }
}
</script>

<style lang="stylus">
.home-table
  width 100%
</style>
