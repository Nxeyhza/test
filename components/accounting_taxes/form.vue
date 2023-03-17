<template>

  <q-card class="q-pa-md q-ma-md">
    <div class="column">
      <q-form ref="form" class="q-gutter-md" >


      <q-input  v-model="formData.tax_name" label="Tax name" type="char" :rules="[ val => val && val.length > 0 || 'Please type something']" />
      <q-input  v-model="formData.tax_rate" label="Tax rate" />
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
    }
  },
  methods: {
    async submitData () {
      let validation = await this.$refs.form.validate(true)
      if(validation){
        alert('Submitting Data to Backend')
      }else{
        alert('Form Validation Failed')
      }
    }
  }
}

</script>
