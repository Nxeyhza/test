<template>
  <div class="q-pa-md">
    <div>
      <h5>Organisation</h5>
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
        { label:'Organisation name',field:'organisation_name' },
        { label:'Prefix', field: 'prefix' },
        { label:'Description', field: 'description'},
        { label:'Address', field: 'address'},
        { label:'State', field: 'state'},
        { label:'City', field: 'city'},
        { label:'Country', field: 'country'},
        { label:'Pin code', field: 'pincode'},
        { label:'Contact number', field: 'contact_number'},
        { label:'Email', field: 'email'},
        { label:'Gst number', field: 'gst_number'},
        { label:'Pan no', field: 'pan_no'},
        { label:'Invoices', field: 'invoices'},
        { label:'Status', field: 'status'},
        { label:'User created', field: 'user_created'},
        { label:'User updated', field: 'user_updated'},
        { label:'Date created', field: 'date_created'},
        { label:'Date updated', field: 'date_updated'},
        { label:'Banks', field: 'banks'},

      ]
      }
    }
  },

  methods: {
    insertData (data) {
      this.table.rows.push(data)
    },
     async fetchData(){
      let response=await this.$api.get('https://gangotri-api.brainysoftwares.com/items/organisation?fields=*.*')
      this.table.rows=response.data.data
    }
  },
  created(){
    this.fetchData()
  }
}

</script>
