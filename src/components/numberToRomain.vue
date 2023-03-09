<template>
  <div class="container-lg">
    <div class="row justify-content-center">
      <form class="col-md-4 bg-light shadow p-4 mt-2" id="app" v-on:submit="convertNumber" ref="form">
        <h4 v-text="msg" class="pb-2"></h4>
        <p v-text="'Please complete the form'" class="pb-2"></p>
        <div class="form-group d-flex w-100 pb-3">
          <div class="pe-3 pt-1">Number</div>
          <input v-model="form.number" v-on:focusin="response={}" required placeholder="Enter a number between 1-100"
                 class="form-control float-lg-end" id="number" type="number" name="number" min="1" max="100">
        </div>
        <p class="alert alert-info pb-3 w-100" v-if="Object.keys(response).length>0 && response.error === false" v-text="'Roamin of '+form.number+' is ' +response.result"></p>
        <p class="alert alert-danger pb-3 w-100" v-if="Object.keys(response).length>0 && response.error===true"  v-text="response.message"></p>
        <div class="w-100">
          <input class="w-25 m-2 btn btn-sm btn-secondary float-lg-start" type="button" v-on:click="cancel" value="cancel">
          <input class="w-25 m-2 btn btn-sm btn-primary float-lg-end" type="submit" value="submit">
        </div>
      </form>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      form: {
        number: undefined
      },
      response: {
      }
    };
  },
  methods: {
    convertNumber: async function (e) {
      e.preventDefault();
      this.response = {};
      this.response = await axios.post(process.env.VUE_APP_API_URL + "/numberToRomain", this.form).then(response => {
        return response.data
      }).catch(error =>{
        return error.response.data
      })
    },
    cancel: function(){
      this.response = {};
      this.form.number=undefined;
      this.$refs.form.reset();
    }
  },
}
</script>

