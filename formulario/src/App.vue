<template>
  <div id="app">
    
    <div class="jumbotron jumbotron-fluid">
      <div class="container">
        <h1 class="display-4">Cadastro de medicamentos</h1>
        <p class="lead">Formulário Althaia Farmacêutica</p>
      </div>
    </div>

    <div class="container">

      <div class="row">

        <!-- formulario -->
        <div class="col-sm-6">

          <h3 class="mt-2">Preencha abaixo</h3>

          <form @submit.prevent="enviar" @reset="resetar">
            
           
            <div class="form-group">
              <label>Apresentação do medicamento</label>
               <input type="text" 
                class="form-control"
                placeholder="Informe o medicamento"
                v-model.lazy.trim="$v.medicamentos.apresentacao.$model" >
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
                v-model.lazy.trim="$v.medicamentos.principio.$model" >
            </div>

            
            <div class="form-group">
              <label>Empresa</label>
              <input type="text"
              class="form-control"
              placeholder="Informe a empresa fabricante"
              v-model.lazy.trim="$v.medicamentos.empresa.$model">
            </div>


            <button class="btn btn-secondary" type="reset">Resetar</button>
            <button class="btn btn-success" type="submit" @click="log" >Enviar</button>

          </form>

        </div>

        <!-- saida -->
        <div class="col-sm-6 ">

          <h3 class="mb-5">Saída</h3>

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

import {required, maxLength} from 'vuelidate/lib/validators'

export default {
  data () {
    return {
      medicamentos: {
        apresentacao: '',
        descricao: '',
        principio: '',
        empresa: ''
      }
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
      required:required,
      maxLength: maxLength(200)
    }
  }
},

  methods: {
    enviar() {
      const formularioEnviado = Object.assign({}, this.medicamentos)
      console.log('formulário enviado!', formularioEnviado);
    },
    resetar() {
      this.medicamentos = Object.assign({}, '')
    },

    log() {
      console.log('Vuelidate: ', this.$v)
    }
  },

  created() {
    this.resetar()
  }


}
</script>

<style scoped>
  .btn {
    margin-right: 5px;
  }
</style>