<template>
  <q-card class="q-pa-md q-ma-md">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md">
      <q-input v-model="formData.vehicle_no" mask="N" reverse-fill-mask label="Vehicle No." :rules="[val => !!val || 'Field is required']" />
      <q-select clearable v-model="formData.vehicle_type" label="Vehicle type" :options="vehicle_type" option-label="vehicle_type"
       option-value="vehicle_type" map-options emit-value  />
      <q-select v-model="formData.status" label="Status" :options="['Published','Draft','Archived']"
       option-label="Standard"   />
      <q-input v-model="formData.sort" label="Sort" />
      <q-input v-model="formData.fuel_avg" label="Fuel Avg" />
      <q-input v-model="formData.log_book" label="Log book" />

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
      vehicle_type: []
    }
  },
  created(){
    this.fetchVehicle()
  },
  methods: {

    async fetchVehicle(){
      let response = await this.$api.get('items/vehicle_type')
      this.vehicle_type = response.data.data
    },
  async  submitData () {
      let validation = await this.$refs.form.validate(true)
      if(validation){
        alert('submitting data to backend')
      } else{
        alert('form validation failed')
      }
      this.formData = {}
    }
  }
}
</script>
