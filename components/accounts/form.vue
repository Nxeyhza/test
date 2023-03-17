<template>
  <q-card class="q-pa-md q-ma-md">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md">

      <q-input  v-model="formData.account_name" label="Account Name *" type="char" :rules="[val=> !!val|| 'field is required']" />
      <q-input  v-model="formData.account_address" label="Account address*" type="char" :rules="[val=> !!val|| 'field is required']"/>
      <q-input v-model="formData.contact_number" mask="##########"  label="Contact number" />
      <div class="row">
      <q-input  class="col" v-model="email" label="Email" />
      <q-select v-model="emailDomain" style="width:100px" :options="['@gmail.com','@outlook.com']"></q-select>

      </div>

      <q-input v-model="formData.city" mask="S" reverse-fill-mask label="City" type="char" />
      <q-input v-model="formData.state" mask="S" reverse-fill-mask label="State" type="char" />
      <q-input v-model="formData.pin_code" mask="######"  label="Pin Code" />
      <q-input v-model="formData.country" mask="S" reverse-fill-mask label="Country" type="char" />
      <q-input v-model="formData.accounting_receipts" label="Accounting Receipts" />
      <q-select v-model="formData.status" label="Status" :options="['Published','Draft','Archived']"
       option-label="Standard"  />
      <q-input v-model="formData.invoices" label="Invoices" />
      <q-input v-model="formData.contacts" label="Contacts" />
      <q-input v-model="formData.log_book" label="Log Book" />
      <q-input v-model="formData.contracts" label="Contracts" />
      <q-input v-model="formData.gst" mask="N" reverse-fill-mask label="GST" />

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
      formData: {}
    }
  },
  computed: {
    emailDomain:{
      set(val){
        this.formData.email = this.email + val
      },
      get(){
        let emailA = this.formData?.email?.split('@') || ['','']
        return emailA?.[1] ? emailA[1] + '@' : ''
      }
    },
    email:{
      set(val){
        this.formData.email =  val + this.emailDomain
      },
      get(){
        let emailA = this.formData?.email?.split('@') || ['','']
        return emailA?.[0] || ''
      }
    }
  },
  methods: {
   async submitData () {
      let validation = await this.$refs.form.validate(true)
      if (validation){
        alert('submitting data to backend')
       }else{
        alert('form validation failed')
       }
      this.formData = {}
    }
  }
}
</script>
