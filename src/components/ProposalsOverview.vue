<template>
  <q-layout>
    <!--
      Replace following "div" with
      "<router-view class="layout-view">" component
      if using subRoutes
    -->
    <div class="layout-view">

      <div class="layout-padding">
        <br/>
        <h5 class="page-title">
            Proposals
            <router-link :to="{ name: 'proposal'}">
                <button class="add-proposal clear primary circular small">
                    <i>add</i>
                    <q-tooltip anchor="center left" self="center right" :offset="[-10,0]">
                        Create new proposal
                    </q-tooltip>
                </button>
            </router-link>
        </h5>

        <div class="card">
        <q-data-table :config="config" :columns="columns" :data="data"> 
            <!-- -->
            <template slot="col-action" scope="cell"> 
                <button class="tbl-btn negative clear" @click="$refs.deleteModal.open()">
                    <i>delete</i>
                    <q-tooltip anchor="center left" self="center right" :offset="[-10,0]">
                        Delete proposal
                    </q-tooltip>
                </button>
                <router-link :to="{ name: 'proposal', query: { id: cell.row.id }}">
                    <button class="tbl-btn primary clear">
                        <i>edit</i>
                        <q-tooltip anchor="center left" self="center right" :offset="[-10,0]">
                            Edit proposal
                        </q-tooltip>
                    </button>
                </router-link>

                <q-modal ref="deleteModal" position="top">
                    <div class="toolbar">                   
                        <q-toolbar-title :padding="1">
                            Delete proposal
                        </q-toolbar-title>
                        <button @click="$refs.deleteModal.close()">
                            <i>close</i>
                        </button>
                    </div>
                    <div class="layout-view">
                        <div class="layout-padding">
                            Are you sure you want to delete this proposal?                         
                        </div>
                        <div class="footer">
                            <div style="float:right">
                                <button class="clear negative" @click="deleteProposal(cell.row.id)">Delete</button>
                                <button class="clear primary" @click="$refs.deleteModal.close()">Cancel</button>
                            </div>
                        </div>
                    </div>
                    
                </q-modal>
            </template>
        </q-data-table>
        </div>

        <router-link :to="{ name: 'proposal'}">
            <button class="secondary">
                <i>add</i>
                <q-tooltip anchor="center right" self="center left" :offset="[10,0]">
                    Create new proposal
                </q-tooltip>
            </button>
        </router-link>

      </div>
    </div>
  </q-layout>
</template>

<script>
export default {
  data () {
    return {
      config: {
        rowHeight: '50px',
        responsive: true,
        /* pagination: {
             rowsPerPage: 15,
             options: [5, 10, 15, 30, 50, 100]
        }, */
        messages: {
          noData: '<i>warning</i> You have no saved proposals.',
          noDataAfterFiltering: '<i>warning</i> No results. Please refine your search terms.'
        },
        labels: {
          rows: 'Rows',
          selected: {
            singular: 'item selected.',
            plural: 'items selected.'
          },
          clear: 'clear',
          search: 'Search',
          all: 'All'
        }
      },
      columns: [
        {
          label: 'Proposal',
          field: 'name',
          width: '70%',
          filter: true,
          sort: true
        },
        {
          label: 'Date',
          field: 'date',
          width: '20%',
          filter: true,
          sort: true
        },
        {
          label: '',
          field: 'action',
          width: '20%'
        }
      ],
      data: [
        { id: '3', name: 'Proposal One', date: '19.4.2017' },
        { id: '2', name: 'Proposal Two', date: '22.3.2017' },
        { id: '1', name: 'Proposal Three', date: '24.2.2017' },
        { id: '12', name: 'Proposal Four', date: '2.1.2017' }
      ]
    }
  },
  methods: {
    editProposal (id) {
      console.log('edit modal ' + id, this.$router)
    },
    deleteProposal (id) {
      console.log('delete modal ' + id)
    }
  }
}
</script>

<style lang="stylus">
.add-proposal
    margin-bottom 3px
    float right
.tbl-btn
    padding 0 5px 0 5px
    min-height 1.7rem
    float right
.q-data-table-toolbar.upper-toolbar.reverse-wrap
    display none

.modal .footer button
    border-radius 0

.q-data-table .q-search-input
    box-shadow none
</style>
