<template>
  <div class="q-pa-md">
    <div>
      <h5>Accounts</h5>
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
        { label:'Account name',field:'account_name' },
        { label:'Account address', field: 'account_address' },
        { label:'Contact number', field: 'contact_number'},
        { label:'Email', field: 'e_mail'},
        { label:'City', field: 'city'},
        { label:'State', field: 'state'},
        { label:'Pin code', field: 'pin_code'},
        { label:'Country', field: 'country'},
        { label:'Accounting receipts', field: 'accounting_receipts'},
        { label:'Status', field: 'status'},
        { label:'User created', field: 'user_created'},
        { label:'User updated', field: 'user_updated'},
        { label:'Invoices', field: 'invoices'},
        { label:'Contacts', field: 'contacts'},
        { label:'Log book', field: 'log_book'},
        { label:'Contracts', field: 'contracts'},
        { label:'Gst', field: 'gst'},
        { label:'Date created', field: 'date_created'},
        { label:'Date updated', field: 'date_updated'},


      ]
      }
    }
  },

  methods: {
    insertData (data) {
      this.table.rows.push(data)
    },
     async fetchData(){
      let response=await this.$api.get('https://gangotri-api.brainysoftwares.com/items/accounts?fields=*.*')
      this.table.rows=response.data.data
    }
  },
  created(){
    this.fetchData()
  }
}

</script>
