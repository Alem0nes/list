<script setup>
import { reactive } from 'vue';
import Cabecalho from './Components/Cabecalho.vue'
import Formulario from './Components/Formulario.vue';
import ListaDeTarefas from './Components/ListaDeTarefas.vue';

  const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: [
      {
        titulo:'estudar es6',
        finalizada:false,
      },
      {
        titulo:'regar as plantas',
        finalizada: false,
      },
      {
        titulo:'Regar as plantas',
        finalizada: true,
      }
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
      return estado.tarefas;
  }
}

  const cadastraTarefa = () => {
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizada: false,
    }
    estado.tarefas.push(tarefaNova);
    estado.tarefaTemp = '';
  }

</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario 
      :tarefaTemp="estado.tarefaTemp" 
      :editaTarefaTemp="evento => estado.tarefaTemp = evento.target.value" 
      :cadastrarTarefa="cadastraTarefa"
      :trocarFiltro="evento => estado.filtro = evento.target.value"
      />
    <ListaDeTarefas :tarefas="getTarefasFiltradas()"/>
  </div>

</template>

    
