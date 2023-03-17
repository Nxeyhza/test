<template>
  <div class="q-pa-md">
    <div>
      <h5>accounting receipts</h5>
    </div>

    <q-table separator="horizontal" :columns="table.columns" :rows="table.rows">
     <template v-slot:body-cell-mobile_number="props">
      <q-td>
      <q-btn v-if="props.value" flat icon="phone" color="primary" type="a" :label="props.value" :href="'tel:' +props.value "></q-btn>
      </q-td>
     </template>

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
        { label: 'id', field: 'id' },
        { label: 'Account id', field: 'account_id' },
        { label: 'Receipt date', field: 'receipt_date' },
        { label: 'Receipt number', field: 'receipt_number' },
        { label: 'Receipt mode', field: 'receipt-mode' },
        { label: 'Receipt amount', field: 'receipt_amount' },
        { label: 'transaction no.', field: 'transaction_number' },
        { label: 'user created', field: 'user_created' },
        { label: 'date created', field: 'date_created' },
        { label: 'user updated', field: 'user_updated' },
        { label: 'receipt status', field: 'receipt_status' },
        { label: 'receipt settlement', field: 'receipt_settlement' },
        { label: 'date updated', field: 'date_updated' },

        ]
      }
    }
  },

  methods: {
    insertData (data) {

      this.table.rows.push(data)
    },
     async fetchData(){
      let response =await this.$api.get('https://gangotri-api.brainysoftwares.com/items/accounting_receipts?fields=*.*')
      this.table.rows=response.data.data
      }
    },
    created(){


      this.fetchData()
    }
    }



</script>
