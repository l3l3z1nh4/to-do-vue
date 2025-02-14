<script setup>
  import { reactive } from "vue";
  import Cabecalho from './components/Header.vue';
  import Formulario from './components/Formulario.vue';
  import Lista from './components/Lista.vue';

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
      <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"/>
      <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa"/>
      <Lista :tarefas="getTarefasFiltradas()"/>
  </div>
</template>


