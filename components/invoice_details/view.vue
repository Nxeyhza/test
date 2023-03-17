<template>
  <div class="q-pa-md">
    <div>
      <h5>Invoice Details</h5>
    </div>

    <q-table separator="horizontal" :columns="table.columns" :rows="table.rows">
    </q-table>
  </div>
</template>

<script>
export default {
  data () {
    return {
      table: {
        rows: [


        ],
        columns: [
        { label:'Id',field:'id' },
        { label:'User created', field: 'user_created'},
        { label:'User updated', field: 'user_updated'},
        { label:'Date created', field: 'date_created'},
        { label:'Date updated', field: 'date_updated'},
        { label:'Item ID',field:'item_id' },
        { label:'Rate', field: 'rate' },
        { label:'Quantity', field: 'quantity'},
        { label:'Amount', field: 'amount'},
        { label:'Tax rate', field: 'tax_rate'},
        { label:'Tax amount', field: 'tax_amount'},
        { label:'Total amount', field: 'total_amount'},
        { label:'Status', field: 'status'},
        { label:'Invoice id', field: 'invoice_id'},
        { label:'Description', field: 'description'},


      ]
      }
    }
  },

  methods: {
    insertData (data) {
      this.table.rows.push(data)
    },
     async fetchData(){
      let response=await this.$api.get('https://gangotri-api.brainysoftwares.com/items/invoice_details?fields=*.*')
      this.table.rows=response.data.data
    }
  },
  created(){
    this.fetchData()
  }
}

</script>
