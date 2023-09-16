<script setup>

import {reactive} from 'vue';

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
  estado.tarefas.push(tarefaNova);
  estado.tarefas.tarefaTemp = '';
}

</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>
        Você possui {{ getTarefasPendentes().length }} Tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input type="text" @change="evento => estado.tarefaTemp = evento.target.value" :value="estado.tarefas.tarefaTemp" required placeholder="Digite aqui a descrição da tarefa" class="form-control">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="todas">Todas as tarefas</option>
            <option value="pendentes">Tarefas Pendentes</option>
            <option value="finalizadas">Tarefas finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li v-for="tarefas in getTarefasFiltradas()" class="list-group-item">
        <input @change="evento => tarefas.finish = evento.target.checked" :checked="tarefas.finish" :id="tarefas.title" type="checkbox">
        <label :class="{done: tarefas.finish}" class="ms-3" :for="tarefas.title">
          {{ tarefas.title }}
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
