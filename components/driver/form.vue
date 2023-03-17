<template>
  <q-card class="q-pa-md q-ma-md">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md">

      <q-input v-model="formData.driver_name" mask="S" reverse-fill-mask label="Driver name" type="char" :rules="[val => !!val || 'Field is required']" />
      <q-input v-model="formData.address" mask="S" reverse-fill-mask label="Address" type="char" />
      <q-input v-model="formData.contact_no" mask="##########" label="Contact no" :rules="[val => !!val || 'Field is required']" />
      <q-select v-model="formData.status" label="Status" :options="['Published','Draft','Archived']"
       option-label="Standard" :rules="[val => !!val || 'Field is required']" />
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
  methods: {
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
