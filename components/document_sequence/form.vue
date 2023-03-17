<template>
  <q-card class="q-pa-md q-ma-md">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md">

      <q-select v-model="formData.organisation_id" label="Organisation ID" :options="organisation" option-label="id"
      option-value="id" map-options emit-value :rules="[val => !!val || 'Field is required']" />
      <q-select v-model="formData.document_type" label="Document Type*" :options="['Invoice','Receipt']"
       option-label="Standard" :rules="[val => !!val || 'Field is required']" />
      <q-input v-model="formData.sequence_no" mask="N" reverse-fill-mask label="Sequence no" />
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
    this.fetchOrg()
  },
  methods: {
    async fetchOrg(){
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
