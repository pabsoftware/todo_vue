<script setup>
import { reactive } from 'vue';

const estado = reactive({
  filtro: 'todas',
  tarefasTemp: '',
  tarefas: [
    {
      titulo: 'Estudar ES6',
      Finalizada: false 
    },
    {
      titulo: 'Estudar SASS',
      Finalizada: false 
    },
    {
      titulo: 'Ir à academia',
      Finalizada: true 
    }
  ]
})

const getTarefasPedentes = () => {
  return estado.tarefas.filter(tarefa => tarefa.Finalizada === false)
}
const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.Finalizada === true)
}

const getTarefasFiltradas = () => {
  const {filtro} = estado;
  switch (filtro) {
    case 'pendedntes':
      return getTarefasPedentes();
    case 'finalizadas':
      return getTarefasFinalizadas();
    
    case 'todos':
      return estado.tarefas;
  }
}

const cadastrarTarefa = () => {
  
  const tarefaNova = {
    titulo: estado.tarefasTemp,
    Finalizada: false,
  }
  estado.tarefas.push(tarefaNova);
  estado.tarefasTemp = ''
}
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4">
      <h1>Minhas tarefas</h1>
      <p>Você possue {{ getTarefasPedentes().length }} tarefas pendentes</p>
    </header>

    <form action="" @submit.prevent="cadastrarTarefa()">
    <div class="row">
      <div class="col">
        <input :value="estado.tarefasTemp" @change="evento => estado.tarefasTemp = evento.target.value " required class="form-control" type="text" placeholder="Digite aqui a descrição da tarefa">
      </div>
      <div class="col-md-2">
        <button class="btn btn-primary">Cadastrar</button>
      </div>
      <div class="col-md-2">
        <select @change="evento => estado.filtro = evento.target.value" class="form-control" name="" id="">
          <option value="todos">Todas as tarefas</option>
          <option value="pendedntes">Todas as pendentes</option>
          <option value="finalizadas">Todas as finalizadas</option>
        </select>
      </div>
    </div>
  </form>

  <ul class="list-group mt-4">
    <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
      <input @change="e => tarefa.Finalizada = e.target.checked" :checked="tarefa.Finalizada" :id="tarefa.titulo" type="checkbox" >
      <label :class="{done: tarefa.Finalizada}" class="ms-3" :for="tarefa.titulo">{{ tarefa.titulo }}</label>
    </li>
  </ul>
  </div>

 
</template>

<style scoped>
.done {
  text-decoration: line-through;
}

</style>
