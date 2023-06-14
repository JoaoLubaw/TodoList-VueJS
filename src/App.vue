<script setup>
import { reactive } from 'vue'
import Cabecalho from './components/Cabecalho.vue'
import Form from './components/Form.vue'
import Lista from './components/Lista.vue'

  const estado= reactive({
    valor1:0,
    valor2:0,
    operacao:'menos',
    resultado:0,
    filtro: 'todas',
    tarefaTemp:'',
    tarefas: [
    ]
  })

  const makeCalc = () => {
    const {operacao} = estado;

    switch(operacao) {
      case 'mais':
        return parseInt(estado.valor1) + parseInt(estado.valor2);
      case 'vezes':
        return estado.valor1 * estado.valor2;
      case 'dividido':
        return estado.valor1 / estado.valor2;
      default:
        return estado.valor1 - estado.valor2;
      }
}

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
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"/>
    <Form :trocarFiltro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa"/>
    <Lista :tarefas="getTarefasFiltradas()" />

  <h3 class="mt-5" >Calculadora</h3>

    <form class="calc mt-3">
      <div class="row">
        <div>
          <input  type="number" placeholder="Insira o primeiro N°" @keyup="evento => estado.valor1 = evento.target.value">
      
          <select class="select" @change="evento => estado.operacao = evento.target.value">
            <option value="menos">-</option>
            <option value="mais">+</option>
            <option value="vezes">x</option>
            <option value="dividido">÷</option>
          </select>
        
          <input type="number" placeholder="Insira o segundo N°" @keyup="evento => estado.valor2 = evento.target.value" >
        </div>

        
        <h5 class="mt-3">={{ makeCalc() }}</h5>
      </div>
    </form>
  </div>

</template>

<style scoped>
.select {
  margin: 0 5px;
}
</style>