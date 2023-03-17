<template>
  <q-card class="q-pa-md q-ma-md">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md">


      <q-select v-model="formData.item_id" label="Item ID" :options="items" option-label="id"
       option-value="id" map-options emit-value />
      <q-input v-model="formData.rate" label="Rate" />
      <q-input clearable v-model="formData.quantity" label="Quantity *" :rules="[val => !!val || 'Field is required']" />
      <q-input clearable v-model="formData.amount" mask="#" reverse-fill-mask label="Amount *" :rules="[val => !!val || 'Field is required']" />
      <q-input v-model="formData.tax_rate"  label="Tax Rate" />
      <q-input v-model="formData.tax_amount" mask="#" reverse-fill-mask label="Tax amount" />
      <q-input v-model="formData.total_amount" label="Total amount" />
      <q-select v-model="formData.status" label="Status" :options="['Published','Draft','Archived']"
       />
      <q-select v-model="formData.invoice_id" label="Invoice ID" :options="invoices" option-label="id"
       option-value="id" map-options emit-value   />
      <q-input v-model="formData.description" mask="S" reverse-fill-mask label="Description" type="char"/>
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
      items:[],
      invoices:[]
    }
  },
  created() {
    this.fetchItem()
    this.fetchInvoice()
  },

  methods: {
    async fetchItem(){
      let response = await this.$api.get('items/items')
      this.items = response.data.data
    },
    async fetchInvoice(){
      let response = await this.$api.get('items/invoices')
      this.invoices = response.data.data
    },
   async submitData () {
      let validation = await this.$refs.form.validate(true)
      if(validation){
        alert('submitting data to backend')
      }else{
        alert('form validation failed')
      }
      this.formData = {}
    }
  }
}
</script>
