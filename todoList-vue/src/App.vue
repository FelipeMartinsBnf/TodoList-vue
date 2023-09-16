<script setup>

import {reactive} from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import List from './components/List.vue'


const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: [
    {title: "Estudar ES6",
    finish: false},
    {title: "Academia",
    finish: true}
  ]
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefas => !tarefas.finish);
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefas => tarefas.finish);
}

const getTarefasFiltradas = () => {
  const {filtro} = estado;

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
    title: estado.tarefaTemp,
    finish: false
  }
  estado.tarefas.tarefaTemp = '';
  estado.tarefas.push(tarefaNova);
}

const deletaTarefa = (id) => {
  if(confirm("Tem certeza que quer deletar a tarefa "+id+"?")){
    for (var i = estado.tarefas.length - 1; i >= 0; --i) {
      if (estado.tarefas[i].title == id) {
        estado.tarefas.splice(i,1);
      }
    }
  }
}

</script>

<template>
  <div class="container" >
      <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
      <Formulario :tarefa-temp="estado.tarefas.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa" :trocar-filtro="evento => estado.filtro = evento.target.value" />
      <List :tarefas="getTarefasFiltradas()" :delete="deletaTarefa" />
  </div>
</template>
