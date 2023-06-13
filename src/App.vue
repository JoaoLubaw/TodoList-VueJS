<script setup>
import { reactive } from 'vue'; 
import Cabecalho from './components/Cabecalho.vue';
import form from './components/form.vue';
import Lista from './components/Lista.vue';

  const estado= reactive({
    filtro: 'todas',
    tarefaTemp:'',
    tarefas: [
    ]
  })

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  }

  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }

  const getTarefasFiltradas = () => {
    const {filtro} = estado;

    switch(filtro) {
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
    <Cabecalho />
    <form />
    <Lista />
  </div>

</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
