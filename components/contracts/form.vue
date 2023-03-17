<template>
  <q-card class="q-pa-md q-ma-md">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q=gutter-md">

      <q-input v-model="formData.name" mask="S" reverse-fill-mask label="Name" type="char" />
      <q-select v-model="formData.account" label="Account"  :options="accounts" option-label="id"
       option-value="id" map-options emit-value :rules="[val => !!val || 'Field is required']" />
      <q-select v-model="formData.vehicle_type" label="vehicle Type"  :options="vehicle_type" option-label="id"
       option-value="id" map-options emit-value :rules="[val => !!val || 'Field is required']"  />
      <q-input v-model="formData.rent_per_month" label="Rent per month" />
      <q-select v-model="formData.fuel" label="Fuel*" :options="['Including','Excluding']"
       option-label="Standard" :rules="[val => !!val || 'Field is required']"/>
      <q-input v-model="formData.log_book" label="Log Book" />
      <q-toggle v-model="formData.is_tax_included" label="Is tax included" :false-value="true"
      :label="`Model is ${redModel} (flipped boolean)`"
      :true-value="false"
      color="red"
      type="redModel"
 />
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
      accounts:[],
      vehicle_type:[]
    }
  },
  created(){
    this.fetchAccounts()
    this.fetchVehicles()
  },

  methods: {
    async fetchAccounts(){
      let response = await this.$api.get('items/accounts')
      this.accounts = response.data.data
    },
    async fetchVehicles(){
      let response = await this.$api.get('items/vehicle_type')
      this.vehicle_type = response.data.data
    },

     async submitData () {
    let validation =await this.$refs.form.validate(true)
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
