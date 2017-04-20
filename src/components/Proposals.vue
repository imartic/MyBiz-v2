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
        <h5 class="page-title">Proposals</h5>

        <div class="card">
        <q-data-table :config="config" :columns="columns" :data="data"> 
            <!-- -->
            <template slot="col-action" scope="cell"> 
                <button class="tbl-btn negative clear" @click="deleteProposal(cell.row.id)">
                    <i>delete</i>
                    <q-tooltip anchor="center left" self="center right" :offset="[-10,0]">
                        Delete proposal
                    </q-tooltip>
                </button>
                <button class="tbl-btn primary clear" @click="editProposal(cell.row.id)">
                    <i>edit</i>
                    <q-tooltip anchor="center left" self="center right" :offset="[-10,0]">
                        Edit proposal
                    </q-tooltip>
                </button>
            </template>
        </q-data-table>
        </div>

      </div>
    </div>
  </q-layout>
</template>

<script>
export default {
  data () {
    return {
        config: {
            // [REQUIRED] Set the row height
            rowHeight: '50px',
            bodyStyle: {
                maxHeight: '500px'
            },
            responsive: true,
            /*pagination: {
                rowsPerPage: 15,
                options: [5, 10, 15, 30, 50, 100]
            },*/
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
            sort: true,
        },
        {
            label: 'Date',
            field: 'date',
            width: '20%',
            filter: true,
            sort: true,
        },
        {
            label: '',
            field: 'action',
            width: '20%',
        }
        ],
        data: [
            { id: '3', name: 'Proposal One', date: '19.4.2017' },
            { id: '2', name: 'Proposal Two', date: '22.3.2017' },
            { id: '1', name: 'Proposal Three', date: '24.2.2017' }
        ]
    }
  },
  methods: {
    conlog (data) {
        console.log('Data: ', data)
    },
    editProposal (id) {
        console.log(id)
    },
    deleteProposal (id) {
        confirm('Delete proposal ' + id + '?')
    }
  }
}
</script>

<style lang="stylus">
.page-title
    padding-bottom 10px
    border-bottom 1px solid #ccc
.tbl-btn
    padding 0 7px 0 7px
    min-height 1.7rem
    float right
.q-data-table-toolbar.upper-toolbar
    display none
</style>
