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

        <q-data-table
            :data="table"
            :config="config"
            :columns="columns"
            @refresh="refresh"
            > <!-- todo: ... -->
            <!-- Custom renderer for "name" column -->
            <template slot="col-name" scope="cell">
                {{cell.data}}
            </template>
            <!-- Custom renderer for "date" column -->
            <template slot="col-date" scope="cell">
                {{cell.data}}
            </template>
        </q-data-table>

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
            pagination: {
                rowsPerPage: 15,
                options: [5, 10, 15, 30, 50, 100]
            },
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
            field: 'string',
            width: '65%',
            filter: true,
            sort: true
        },
        {
            label: 'Date',
            field: 'isodate',
            width: '35%',
            filter: true,
            sort: true
        }
        ],
        table: [
            { name: 'Proposal One', date: '12-4-2017' },
            { name: 'Proposal Two', date: '22.3.2017' },
            { name: 'Proposal Three', date: '10.2.2017' }
        ]
    }
  },
  methods: {
    refresh () {

    }
  }
}
</script>

<style lang="stylus">
.page-title
    padding-bottom 10px
    border-bottom 1px solid #ccc
</style>
