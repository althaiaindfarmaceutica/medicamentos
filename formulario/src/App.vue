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

          <form>
            
            <div class="form-group">
              <label>Apresentação</label>
              <textarea class="form-control" placeholder="Apresentação do medicamento"></textarea>
            </div>

             <div class="form-group">
              <label>Descrição</label>
              <textarea class="form-control" placeholder="Descrição do medicamento"></textarea>
            </div>

            <div class="form-group">
              <label>Princípio ativo</label>
              <input type="text" class="form-control" placeholder="Informe o nome do princípio ativo">
            </div>

            
            <div class="form-group">
              <label>Empresa</label>
              <input type="text" class="form-control" placeholder="Informe a empresa fabricante">
            </div>


            <button class="btn btn-secondary">Resetar</button>
            <button class="btn btn-success">Enviar</button>

          </form>

        </div>

        <!-- saida -->
        <div class="col-sm-6">

          <h3 class="mb-5">Saída</h3>

          <div class="card">

            <div class="card-header">Dados preenchidos</div>

            <ul class="list-group list-group-flush">
              <li class="list-group-item"><strong>Apresentação:</strong></li>
              <li class="list-group-item"><strong>Descrição:</strong> </li>
              <li class="list-group-item"><strong>Princípio Ativo:</strong></li>
              <li class="list-group-item"><strong>Empresa:</strong> </li>
            </ul>


            <!-- 
            <div class="card-header">Model</div>
              <div class="card-body">
              <pre><code>{{ {'nome': 'Plínio Naves'} }}</code></pre>
            </div> -->

          </div>

        </div>

      </div>

    </div>

  </div>
</template>


<style scoped>
  .btn {
    margin-right: 5px;
  }
</style>