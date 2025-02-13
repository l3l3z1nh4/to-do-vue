<script setup>
import { reactive } from "vue";

const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: [
    {
      titulo:'estudar',
      finalizado: false,
    },
    {
      titulo:'fazer unha',
      finalizado: false,
    },
    {
      titulo: 'lavar o cabelo',
      finalizado: true,
    }
  ]
});

//funções
const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizado)
}
const getTarefasConcluidas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizado)
}

const getTarefasFiltradas = () => {
  const {filtro} = estado;

  switch (filtro){
    case 'pendentes':
      return getTarefasPendentes();
    case 'concluidas':
      return getTarefasConcluidas();
    default:
      return estado.tarefas;
  }
}

const cadastraTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    finalizado: false
  }
  estado.tarefas.push(tarefaNova);
  estado.tarefaTemp = '';
}

</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 bg-light rounded-3">
      <h1>minhas tarefas</h1>
      <p>{{ getTarefasPendentes().length}} pendentes</p>
    </header>
    <form @submit.prevent="cadastraTarefa()">
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemp"  @change=" evento => estado.tarefaTemp = evento.target.value" required type="text" placeholder="adicionar tarefa" class="form-control">
        </div>
        <div class="col-md-1">
        <button type="submit" class="btn btn-primary">+</button>
      </div>
      <div class="col-md-2">
        <select @change=" evento => estado.filtro = evento.target.value" class="form-control">
          <option value="todas">Todas as tarefas</option>
          <option value="pendentes">Tarefas pendentes</option>
          <option value="concluidas">Tarefas concluidas</option>
        </select>
      </div>
      </div> 
    </form>


    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
        <input @change=" evento => tarefa.finalizado = evento.target.checked " :checked="tarefa.finalizado" :id="tarefa.titulo" type="checkbox">
        <label :class="{ done: tarefa.finalizado}" class="ms-2" :for="tarefa.titulo">{{tarefa.titulo}}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
  .done{
    text-decoration: line-through;
  }
</style>
