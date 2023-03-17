<template>
  <q-card class="q-pa-md q-ma-md">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md">

      <q-select clearable v-model="formData.account_id" label="Account Id" :options="accounts" option-label="id"
       option-value="id" map-options emit-value :rules="[val => !!val || 'Field is required']" />
      <q-input v-model="formData.designation" mask="S" reverse-fill-mask label="Designation" type="char" />
      <q-input v-model="formData.name" mask="S" reverse-fill-mask label="Name" type="char" :rules="[val => !!val || 'Field is required']" />
      <q-select v-model="formData.status" label="Status" :options="['Published','Draft','Archived']"
       option-label="Standard" />
      <q-input v-model="formData.sort" label="Sort" />
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
      accounts:[]
    }
  },
  created () {
    this.fetchAccounts()
  },
  methods: {
    async fetchAccounts(){
      let response = await this.$api.get('items/accounts')
      this.accounts=response.data.data
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
