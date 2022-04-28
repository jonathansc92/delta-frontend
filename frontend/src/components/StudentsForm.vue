<template>
  <div class="studentsForm loader" v-if="loading">
      <h1> {{ title }} </h1>

      <form>
        <div class="mb-3">
          <div class="form-group">
            <label for="exampleFormControlFile1">Example file input</label>
            <input type="file" class="form-control-file" id="exampleFormControlFile1">
          </div>
        </div>
        <div class="mb-3">
          <label for="exampleInputEmail1" class="form-label">Nome</label>
          <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
          <div id="emailHelp" class="form-text">We'll never share your email with anyone else.</div>
        </div>
        <div class="row">
          <div class="col-md-3">
            <label for="exampleInputEmail1" class="form-label">CEP</label>
            <input type="text" class="form-control" v-model="cep" @keyup="searchCep()" placeholder="digite o cep aqui">
          </div>
          <div class="col-md-3">
             <label for="exampleInputEmail1" class="form-label">Cidade</label>
            <input type="email" class="form-control" v-model="form.city" id="exampleInputEmail1" aria-describedby="emailHelp">
          </div>
          <div class="col-md-3">
            <label for="exampleInputEmail1" class="form-label">Estado</label>
            <input type="email" class="form-control" v-model="form.state" id="exampleInputEmail1" aria-describedby="emailHelp">
          </div>
          <div class="col-md-3">
            <label for="exampleInputEmail1" class="form-label">Número</label>
            <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
          </div>
        </div>  
        <div class="row">
          <div class="col-md-6">
            <label for="exampleInputEmail1" class="form-label">Logradouro</label>
            <input type="email" class="form-control"  v-model="form.street" id="exampleInputEmail1" aria-describedby="emailHelp">
          </div>
          <div class="col-md-6">
            <label for="exampleInputEmail1" class="form-label">Bairro</label>
            <input type="email" class="form-control"  v-model="form.district" id="exampleInputEmail1" aria-describedby="emailHelp">
          </div>
        </div>
        <div class="mb-3">
          </div>
        <div class="mb-3">
          <label for="exampleInputEmail1" class="form-label">Complemento</label>
          <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
          <div id="emailHelp" class="form-text">We'll never share your email with anyone else.</div>
        </div>
       
        {{data}}
      </form>

  </div>
</template>

<script>
import axios from "axios";

export default {
  name: 'StudentsForm',
  props: {
    msg: String,
    title: String
  },
  data() {
      return {
        form: {
          email: '',
          name: '',
          state: null,
          district: null,
          street: null,
          city: null,
        },
        data: Object,
        cep: null,
        loading: true
      }
    },
  methods: {
    searchCep () {
      if(this.cep.length == 8) {
        console.log('io')
        axios.get(`https://viacep.com.br/ws/${ this.cep }/json/`)
          .then( 
            response => this.data = response.data,

            this.form.district = this.data.bairro,
            this.form.state = this.data.uf,
            this.form.street = this.data.logradouro,
            this.form.city = this.data.localidade,
          )
          .catch( error => console.log(error) )
      }
		}
  }
}
</script>

