<script setup>
    const props = defineProps(['cadastrarTarefa', 'tarefaTemp', 'trocarFilto', 'editaTarefaTemp'])
</script>

<template>
    <form action="" @submit.prevent="props.cadastrarTarefa">
   <div class="row">
     <div class="col">
       <input :value="props.tarefaTemp" @change="props.editaTarefaTemp " required class="form-control" type="text" placeholder="Digite aqui a descrição da tarefa">
     </div>
     <div class="col-md-2">
       <button class="btn btn-primary">Cadastrar</button>
     </div>
     <div class="col-md-2">
       <select @change="props.trocarFilto" class="form-control" name="" id="">
       <option value="todos">Todas as tarefas</option>
       <option value="pendedntes">Todas as pendentes</option>
       <option value="finalizadas">Todas as finalizadas</option>
       </select>
     </div>
   </div>
 </form>

 </template>