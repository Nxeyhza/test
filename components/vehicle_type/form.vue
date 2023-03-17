<template>
  <q-card class="q-pa-md q-ma-md">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md">

      <q-input v-model="formData.sort"  label="Sort" />
      <q-input v-model="formData.vehicle_type" mask="S" reverse-fill-mask label="Vehicle type" type="char" :rules="[val => !!val || 'Field is required']" />
      <q-input v-model="formData.vehicles" label="Vehicles"   />
      <q-input v-model="formData.contracts" label="Contracts"  />
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
