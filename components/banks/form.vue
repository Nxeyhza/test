<template>
  <q-card class="q-pa-md q-ma-md">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md">

      <q-input v-model="formData.sort" label="Sort" />
      <q-input v-model="formData.bank_name" mask="S" reverse-fill-mask label="Bank name" type="char"  />
      <q-input v-model="formData.account_name" mask="S" reverse-fill-mask label="Account Name" type="char" />
      <q-input v-model="formData.account_no" mask="N" reverse-fill-mask label="Account no" :rules="[val => !!val || 'Field is required']"/>
      <q-input v-model="formData.ifsc" mask="N" reverse-fill-mask label="IFSC" :rules="[val => !!val || 'Field is required']" />
      <q-input v-model="formData.branch" mask="S" reverse-fill-mask label="Branch" type="char" :rules="[val => !!val || 'Field is required']" />
      <q-select clearable v-model="formData.organisation_id" label="Organisation ID" :options="organisation" option-label="id"
       option-value="id" map-options emit-value  />
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
      organisation:[]
    }
  },
  created(){
    this.fetchOrganisation()
  },
  methods: {
    async fetchOrganisation(){
      let response = await this.$api.get('items/organisation')
      this.organisation = response.data.data
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
