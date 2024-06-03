<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';


const estado = reactive({
  filtro: 'todas',
  taefaTemp: '',
  tarefas: [
    {
      titulo: 'Estudar ES6',
      finalizada: false
    },
    {
      titulo: 'Estudar SCSS',
      finalizada: false
    },
    {
      titulo: 'Estudar ES6',
      finalizada: true
    },

  ]
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
}

const getTarefasFiltradas = () => {
  const { filtro } = estado;

  switch (filtro) {
    case 'pendentes':
      return getTarefasPendentes();
    case 'finalizadas':
      return getTarefasFinalizadas();
    default:
      return estado.tarefas
  }
}
const cadastrarTarefa = () => {
  //e.preventDefault()
  const tarefaNova = {
    titulo: estado.taefaTemp,
    finalizada: false
  }

  estado.tarefas.push(tarefaNova)
  estado.taefaTemp = ''
}

</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.taefaTemp" :edita-tarefa-temp="evento => estado.taefaTemp = evento.target.value" :cadastrar-tarefa="cadastrarTarefa"/>
    <ListaDeTarefas :tarefas="getTarefasFiltradas()"/>

  </div>

</template>


