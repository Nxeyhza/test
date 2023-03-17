<template>
  <div class="q-pa-md">
    <div>
      <h5>Accounting Taxes</h5>
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
        { label:'Tax name',field:'tax_name' },
        { label:'Tax rate', field: 'tax_rate' },
        ]
      }
    }
  },
  methods: {
    insertData (data) {
      this.table.rows.push(data)
    },
     async fetchData(){
      let response=await this.$api.get('https://gangotri-api.brainysoftwares.com/items/accounting_taxes?fields=*.*')
      this.table.rows=response.data.data
    }
  },
  created(){
    this.fetchData()
  }
}
</script>
