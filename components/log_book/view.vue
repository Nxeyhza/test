<template>
  <div class="q-pa-md">
    <div>
      <h5>Log Book</h5>
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
        { label:'Vehicle id', field: 'vehicle_id' },
        { label:'Contract id', field: 'contract_id'},
        { label:'Date from', field: 'date_from'},
        { label:'Contact id', field: 'contact_id'},
        { label:'Driver id', field: 'driver_id'},
        { label:'Log type', field: 'log_type'},
        { label:'Date to', field: 'date_to'},
        { label:'Rent', field: 'rent'},
        { label:'Initial reading', field: 'initial_reading'},
        { label:'Final reading', field: 'final_reading'},
        { label:'Running kms', field: 'running_kms'},
        { label:'Oncalldetails', field: 'on_call_details'},
        { label:'Extra kms', field: 'extra_kms'},
        { label:'Days', field: 'days'},
        { label:'Night halt charges', field: 'night_halt_charges'},
        { label:'Amount', field: 'amount'},
        { label:'Status', field: 'status'},
        { label:'Is invoiced', field: 'is_invoiced'},
        { label:'Is paid', field: 'is_paid'},
        { label:'Sort', field: 'sort'},
        { label:'User created', field: 'user_created'},
        { label:'User updated', field: 'user_updated'},
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
      let response=await this.$api.get('https://gangotri-api.brainysoftwares.com/items/log_book?fields=*.*')
      this.table.rows=response.data.data
    }
  },
  created(){
    this.fetchData()
  }
}

</script>
