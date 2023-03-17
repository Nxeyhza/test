<template>
  <div class="q-pa-md">
    <div>
      <h5>Document Sequence</h5>
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
        { label:'Date created',field:'date_created' },
        { label:'Organisation id', field: 'organisation_id' },
        { label:'Document type',field:'document_type' },
        { label:'Sequence no',field:'sequence_no' },

        ]
      }
    }
  },
  methods: {
    insertData (data) {
      this.table.rows.push(data)
    },
     async fetchData(){
      let response=await this.$api.get('https://gangotri-api.brainysoftwares.com/items/document_sequence?fields=*.*')
      this.table.rows=response.data.data
    }
  },
  created(){
    this.fetchData()
  }
}
</script>
