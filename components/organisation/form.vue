<template>
  <q-card class="q-pa-md q-ma-md">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md">

      <q-input v-model="formData.organisation_name" mask="S" reverse-fill-mask label="Organisation Name" type="char" />
      <q-input v-model="formData.prefix" mask="S" reverse-fill-mask label="Prefix*" :rules="[val => !!val || 'Field is required']" />
      <q-input v-model="formData.description" mask="S" reverse-fill-mask label="Description" type="char"/>
      <q-input v-model="formData.address"  label="Address" type="textarea"/>
      <q-input v-model="formData.city" mask="S" reverse-fill-mask label="City" type="char" />
      <q-input v-model="formData.state" mask="S" reverse-fill-mask label="State" type="char" />
      <q-input v-model="formData.pin_code" mask="######" label="Pin code" />
      <q-input v-model="formData.contact_number" mask="##########" label="Contact" />
      <q-input v-model="formData.email" label="Email" type="email" />
      <q-input v-model="formData.gst_number" mask="N" reverse-fill-mask label="GST number"  />
      <q-input v-model="formData.pan_no" mask="N" reverse-fill-mask label="PAN no" />
      <q-input v-model="formData.invoices" label="Invoices" />
      <q-select clearable v-model="formData.status" label="status" :options="['Public','Draft','Archieved']" />
      <q-input v-model="formData.banks" label="banks" />
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
