<template>
  <q-card class="q-pa-md q-ma-md">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md">
      <q-select clearable v-model="formData.account_id" label="Account ID"  :options="accounts" option-label="id"
       option-value="id" map-options emit-value :rules="[val => !!val || 'Field is required']" />
      <q-input  v-model="formData.receipt_date" stack-label label="Receipt Date *" type="date" :rules="[val => !!val || 'Field is required']" />
      <q-input  v-model="formData.receipt_number"  label="Receipt Number *"  :rules="[val => !!val || 'Field is required']" />
      <q-select v-model="formData.receipt_mode" label="Receipt Mode *" :options="['Cheque','Cash','Bank transfer','UPI']"
       option-label="Standard" :rules="[val => !!val || 'Field is required']"  />
      <q-input v-model="formData.receipt_amount" mask="#" reverse-fill-mask label="Receipt Amount *" :rules="[val => !!val || 'Field is required']" />
      <q-input v-model="formData.transaction_number" mask="#" reverse-fill-mask label="Transaction number" />
      <q-select v-model="formData.receipt_status" label="Receipt Status" :options="['Received','Cleared','Declined']"
       option-label="Standard"  />
      <q-input v-model="formData.receipt_settlement" label="Receipt settlement" />
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
      accounts: []
    }
  },
  created (){
    this.fetchAccounts()
  },
  methods: {
    async fetchAccounts(){
      let response = await this.$api.get('items/accounts')
      this.accounts = response.data.data

    },
   async submitData () {
      let validation = await this.$refs.form.validate(true)
      if(validation){
        alert('submitting data to backend')
      }else{
        alert('Form validation failed')
      }
      this.formData = {}
    }
  }
}
</script>
