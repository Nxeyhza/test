<template>
  <q-card class="q-pa-md q-ma-md">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md">

      <q-select v-model="formData.account_id" label="Account ID" :options="accounts" option-label="account_name"
       option-value="id" map-options emit-value :rules="[val => !!val || 'Field is required']" />
      <q-input v-model="formData.invoice_number" mask="#" reverse-fill-mask label="Invoice number" :rules="[val => !!val || 'Field is required']" />
      <q-input clearable v-model="formData.invoice_date" stack-label label="Invoice date*" type="date" :rules="[val => !!val || 'Field is required']" />
      <q-input v-model="formData.grand_total" label="Grand total" />
      <q-select v-model="formData.invoice_status" label="Invoice status" :options="['Draft','Provisional','Final','Cancelled','']"
       option-label="Standard"  />
      <q-select v-model="formData.payment_status" label="Payment Status*" :options="['Unpaid','Partially paid','Paid']"
      option-label="Standard" :rules="[val => !!val || 'Field is required']" />
      <q-select v-model="formData.organisation_id" label="Organisation ID" :options="organisation" option-label="id"
      option-value="id" map-options emit-value />
      <q-input v-model="formData.invoice_details" label="Invoice Details" />
      <q-input v-model="formData.invoice_settlement" label="Invoice settlment" />
      <q-input v-model="formData.period" label="Period" />
      <q-select clearable v-model="formData.bank_id" label="Bank ID" :options="banks" option-label="id"
      option-value="id" map-options emit-value />
      <q-input v-model="formData.booked_by" mask="S" reverse-fill-mask label="Booked by" />
      <q-input v-model="formData.oncall_plan" mask="S" reverse-fill-mask label="Oncall plan" />
      <q-input v-model="formData.vehicle_number" mask="N" reverse-fill-mask label="Vehicle number" />
      <q-input v-model="formData.log_type" mask="S" reverse-fill-mask label="Log type" type="char" />
      <q-input clearable v-model="formData.journey_date" stack-label label="Journey date" type="date" />
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
      accounts: [],
      organisation:[],
      banks: []
    }
  },
  created () {
    this.fetchAccounts()
    this.fetchOrg()
    this.fetchBank()
  },
  methods: {

   async fetchAccounts(){
      let response = await this.$api.get('items/accounts')
      this.accounts = response.data.data
    },
    async fetchOrg(){
      let response = await this.$api.get('items/organisation')
      this.organisation = response.data.data
    },
    async fetchBank(){
      let response = await this.$api.get('items/banks')
      this.banks = response.data.data
    },
   async submitData () {
      let validation = await this.$refs.form.validate('true')
      if(validation){
        alert('submitting data to backend')
      }else{
        alert('form vaidation failed')
      }
      this.formData = {}
    }
  }
}
</script>
