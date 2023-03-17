<template>
  <q-card class="q-pa-md q-ma-md">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md">

      <q-select v-model="formData.invoice_id" label="Invoice ID"  :options="invoices" option-label="id"
       option-value="id" map-options emit-value />
      <q-select v-model="formData.receipt_id" label="Receipt ID"  :options="accounting_receipts" option-label="id"
       option-value="id" map-options emit-value />
      <q-input v-model="formData.amount" mask="#" reverse-fill-mask label="Amount *" :rules="[val => !!val || 'Field is required']" />
</q-form>

    </div>
    <div class="q-py-md">
      <q-btn color="red" label="submit" @click="submitData"></q-btn>
    </div>
    <div class="q-py-md">
      <q-btn color="red" label="close" to="./"></q-btn>
    </div>
  </q-card>

</template>
<script>

export default {
  data () {
    return {
      formData: {},
      invoices: [],
      accounting_receipts: []
    }
  },
  created(){
    this.fetchInvoice()
    this.fetchReceipts()
  },
  methods: {
    async fetchInvoice(){
      let response = await this.$api.get('items/invoices')
      this.invoices = response.data.data
    },
    async fetchReceipts(){
      let response = await this.$api.get('items/accounting_receipts')
      this.accounting_receipts = response.data.data
    },
    async submitData () {
      let validation= await this.$refs.form.validate(true)
      if(validation){
        alert('submitting data to backend')
      } else{
        alert('form validation failed')
      }
      this.formData = {}
    }
  }
}
</script>
