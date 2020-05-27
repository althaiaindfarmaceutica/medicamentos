<template>
  <div id="app">
    
    <div class="jumbotron jumbotron-fluid bg-dark">
      <div class="container">
        <h1 class="display-4 text-light">Cadastro de medicamentos</h1>
        <p class="lead text-light">Formulário Althaia Indústria Farmacêutica</p>
      </div>
    </div>

    <div class="container">

      <div class="row">

        <!-- formulario -->
        <div class="col-sm-6">

          <h3 class="mt-2">Preencha abaixo</h3>

          <form @submit.prevent="enviarForm" @reset="resetar" method="post">
            
              <div v-if="errors.length" class="alert alert-danger" role="alert" >
                <b>Por favor, corrija o(s) seguinte(s) erro(s):</b> <br><br>
                <ul>
                  <li v-for="error in errors" v-bind:key="error.id">{{ error }}</li>
                </ul>
              </div>
           
            <div class="form-group">
              <label>Apresentação do medicamento</label>
               <input type="text" 
                class="form-control"
                placeholder="Informe o medicamento"
                v-model.trim="$v.medicamentos.apresentacao.$model"
                >
            </div>

            <div class="form-group">
              <label>Descrição</label>
              <textarea class="form-control" 
              placeholder="Descrição do medicamento" 
              v-model.lazy.trim="$v.medicamentos.descricao.$model">
              </textarea>
            </div>

            <div class="form-group">
              <label>Princípio ativo</label>
               <input type="text" 
                class="form-control"
                placeholder="Informe o nome do princípio ativo"
                v-model.lazy.trim="$v.medicamentos.principio.$model"
                >
            </div>

            
            <div class="form-group">
              <label>Empresa</label>
              <input type="text"
              class="form-control"
              placeholder="Informe a empresa fabricante"
              v-model.lazy.trim="$v.medicamentos.empresa.$model">
            </div>



            <button class="btn btn-secondary" type="reset">Resetar</button>
            <button class="btn btn-success" type="submit" @click="checkForm">Enviar</button>

          </form>

        </div>

        <!-- saida -->
        <div class="col-sm-6 ">

          <h3 class="mt-2 mb-4">Saída</h3>

          <div class="card">

            <div class="card-header">Dados preenchidos  </div>

            <ul class="list-group list-group-flush">
              <li class="list-group-item"><strong>Apresentação:</strong>  {{ medicamentos.apresentacao}}  </li>
              <li class="list-group-item"><strong>Descrição:</strong> <pre> {{ medicamentos.descricao}} </pre> </li>
              <li class="list-group-item"><strong>Princípio Ativo:</strong> {{ medicamentos.principio}}</li>
              <li class="list-group-item"><strong>Empresa:</strong> {{ medicamentos.empresa}}</li>
            </ul>


             
            <div class="card-header">Model</div>
              <div class="card-body">
              <pre><code>{{ medicamentos }}</code></pre>
            </div> 

          </div>

        </div>

      </div>

    </div>

  </div>
</template>

<script>

import {required,  maxLength} from 'vuelidate/lib/validators'

export default {
  data () {
    return {
      medicamentos: {
        apresentacao: null,
        descricao: null,
        principio: null,
        empresa: null,
      },

        errors: []  
    }
  },

validations: {
  medicamentos: {
    apresentacao: {
      required: required,
      maxLength: maxLength(200)
    },
    descricao: {
      maxLength: maxLength(500)
    },
    principio: {
      required: required,
      maxLength: maxLength(200)
    },
    empresa: {
      required: required,
      maxLength: maxLength(200),
  
    }
  }
},

mounted(){

if(localStorage.getItem('medicamentos')) {
    this.medicamentos = JSON.parse(localStorage.getItem('medicamentos'));  
}

},

  methods: {
    enviarForm() {

      const formularioEnviado = JSON.stringify(this.medicamentos);
      localStorage.setItem('medicamentos', formularioEnviado);
      console.log('formulário enviado!', formularioEnviado);
      
    },
    resetar() {
      this.medicamentos = Object.assign({}, '')
    },

    log() {
      console.log('Vuelidate teste: ', this.$v)
    },
    checkForm() {
        if(this.medicamentos.apresentacao && this.medicamentos.principio && this.medicamentos.empresa){
          alert('Medicamento cadastrado com sucesso!')
          return true;
        }
  
        this.errors = [];
  
        if(!this.medicamentos.apresentacao) {
          this.errors.push('O campo apresentação é obrigatório!');
        }
        
        if(!this.medicamentos.principio) {
          this.errors.push('O campo princípio ativo é obrigatório!');
        }
        
        if(!this.medicamentos.empresa) {
          this.errors.push('O campo empresa é obrigatório!');
        }
  
      
    },

  created() {
    this.resetar()
  }
  },



  


}
</script>

<style scoped>
  .btn {
    margin-right: 5px;
  }
</style>