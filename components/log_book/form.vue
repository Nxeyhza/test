<template>
  <q-card class="q-pa-md q-ma-md">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md">

      <q-input v-model="formData.account_id" label="Account ID" />
      <q-input v-model="formData.vehicle_id" label="Vehicle ID" />
      <q-input v-model="formData.contract_id" label="Contract ID" />
      <q-input clearable v-model="formData.date_from" stack-label label="Date from*" type="date" :rules="[val => !!val || 'Field is required']" />
      <q-input v-model="formData.contact_id" label="Contact ID" />
      <q-input v-model="formData.driver_id" label="Driver ID" />
      <q-select clearable v-model="formData.log_type" label="Log type*" :options="['Monthly','Oncall']"
       option-label="Standard" :rules="[val => !!val || 'Field is required']" />
      <q-input clearable v-model="formData.date_to" stack-label label="Date to*" type="date" :rules="[val => !!val || 'Field is required']" />
      <q-input v-model="formData.rent" label="Rent" />
      <q-input v-model="formData.initial_reading" label="Initial reading" />
      <q-input v-model="formData.final_reading" label="Final reading" />
      <q-input v-model="formData.running_kms" label="Running kms" />
      <q-input v-model="formData.on_call_details" label="On call details" />
      <q-input v-model="formData.extra_kms" label="Extra kms" />
      <q-input v-model="formData.days" mask="#" reverse-fill-mask label="Days" />
      <q-input v-model="formData.night_halt_charges" label="Night halt charges" />
      <q-input v-model="formData.amount" mask="#" reverse-fill-mask label="Amount" />
      <q-select v-model="formData.status" label="Status" :options="['Published','Draft','Archived']"
       option-label="Standard"  />
      <q-toggle v-model="formData.is_invoiced" label="Is invoiced" :false-value="true"
      :label="`Model is ${redModel} (flipped boolean)`"
      :true-value="false"
      color="primary"
      type="redModel"
 />
      <q-toggle v-model="formData.is_paid" label="Is paid" :false-value="true"
      :label="`Model is ${redModel} (flipped boolean)`"
      :true-value="false"
      color="primary"
      type="redModel"
 />
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
      formData: {}
    }
  },
  methods: {
  async  submitData () {
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
