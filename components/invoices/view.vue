<template>
  <div class="q-pa-md">
    <div>
      <h5>Invoices</h5>
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
        { label:'Account id',field:'account_id' },
        { label:'Invoice number', field: 'invoice_number' },
        { label:'invoice date', field: 'invoice_date'},
        { label:'Grand total', field: 'grand_total'},
        { label:'Invoice status', field: 'invoice_status'},
        { label:'Payment status', field: 'payment_status'},
        { label:'User created', field: 'user_created'},
        { label:'User updated', field: 'user_updated'},
        { label:'Date created', field: 'date_created'},
        { label:'Date updated', field: 'date_updated'},
        { label:'Organisation id', field: 'organisation_id'},
        { label:'Invoice details', field: 'invoice_details'},
        { label:'Invoice settlement', field: 'invoice_settlement'},
        { label:'Period', field: 'period'},
        { label:'Bank id', field: 'bank_id'},
        { label:'Booked by', field: 'booked_by'},
        { label:'Oncall plan', field: 'oncall_plan'},
        { label:'Vehicle number', field: 'vehicle_number'},
        { label:'Log type', field: 'log_type'},
        { label:'Journey date', field: 'journey_date'},


      ]
      }
    }
  },

  methods: {
    insertData (data) {
      this.table.rows.push(data)
    },
     async fetchData(){
      let response=await this.$api.get('https://gangotri-api.brainysoftwares.com/items/invoices?fields=*.*')
      this.table.rows=response.data.data
    }
  },
  created(){
    this.fetchData()
  }
}

</script>
