<template>
  <q-card class="q-pa-md q-ma-md">
    {{ formData }}
    <div class="column">
      <q-form ref="form" class="q-gutter-md">

      <q-input v-model="formData.item_name" mask="S" reverse-fill-mask label="Item Name *" type="char" :rules="[val => !!val || 'Field is required']" />
      <q-select clearablerable v-model="formData.item_type" label="Item type" :options="['service','Service with rate']"
       option-label="Standard"  />
      <q-select clearable v-model="formData.status" label="Status" :options="['Published','Draft','Archived']"
       option-label="Standard"  />
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
