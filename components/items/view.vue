<template>
  <div class="q-pa-md">
    <div>
      <h5>Items</h5>
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
        { label:'Item name',field:'item_name' },
        { label:'Item type', field: 'item_type' },
        { label:'Status', field: 'status' },
        { label:'User created', field: 'user_created' },
        { label:'Date created', field: 'date_created' },
        { label:'User updated', field: 'user_updated' },
        { label:'Date updated', field: 'date_updated' },

        ]
      }
    }
  },
  methods: {
    insertData (data) {
      this.table.rows.push(data)
    },
     async fetchData(){
      let response=await this.$api.get('https://gangotri-api.brainysoftwares.com/items/items?fields=*.*')
      this.table.rows=response.data.data
    }
  },
  created(){
    this.fetchData()
  }
}
</script>
