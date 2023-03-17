<template>
  <div class="q-pa-md">
    <div>
      <h5>Vehicle Type</h5>
    </div>

    <q-table separator="horizontal" :columns="table.columns" :rows="table.rows">
    </q-table>
  </div>
</template>

<script>

export default {
  data() {
    return{
      table: {
        rows: [

        ],
        columns: [
        { label:'Id',field:'id' },
        { label:'Sort',field:'sort' },
        { label:'Date created',field:'date_created' },
        { label:'Date updated',field:'date updated' },
        { label:'Vehicle type',field:'vehicle_type' },
        { label:'Vehicles',field:'vehicles' },
        { label:'Contracts',field:'contracts' },

        ]
      }
    }
  },
  methods: {
    insertData (data) {
      this.table.rows.push(data)
    },
     async fetchData(){
      let response=await this.$api.get('https://gangotri-api.brainysoftwares.com/items/vehicle_type?fields=*.*')
      this.table.rows=response.data.data
    }
  },
  created(){
    this.fetchData()
  }
}
</script>
