<script setup>
  import {reactive} from 'vue';
  import Cabecalho from './components/Cabecalho.vue';
  import Formulario from './components/Formulario.vue';
  import ListaTarefas from './components/ListaTarefas.vue';

  const estado = reactive({
    filtro : 'Todas',
    tarefaTemp: '',
    tarefas : [
      {
        titulo: 'Estuda ES6',
        finalizada: false,
      },
      {
        titulo: 'Estudar SASS',
        finalizada: false,
      },
      {
        titulo: 'Ir para academia',
        finalizada: true,
      }
    ]
  })

  const getTarefaPendente = () => {
    //                            ' !tarefa.finalizada ' é a mesma coisa de ' tarefa.finalizada === false '.
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  }

  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }

  const getTarefasFiltradas = () => {
    const { filtro } = estado;

    switch (filtro) {
      case 'Pendentes':
        return getTarefaPendente();
      case 'Finalizadas':
        return getTarefasFinalizadas();
      default:
        return estado.tarefas;
    }
  }

  const cadastraNovaTarefa = () => {
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
    <Cabecalho :tarefas-pendentes="getTarefaPendente().length"/>
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraNovaTarefa" />
    <ListaTarefas :tarefas="getTarefasFiltradas()"/>
  </div>
</template>