<script setup>
    const props = defineProps(['cadastraTarefa', 'tarefaTemp', 'trocarFiltro', 'editaTarefaTemp'])
</script>

<template>
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row">
            <div class="col">
                <input type="text" @change="props.editaTarefaTemp"
                    :value="props.tarefaTemp" required placeholder="Digite aqui a descrição da tarefa"
                    class="form-control">
                {{ props.tarefaTemp }}
            </div>
            <div class="col-md-2 col-sm-12 ">
                <button type="submit" class="btn btn-dark w-100 m-md-0 mt-sm-2 mb-sm-2">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select @change="props.trocarFiltro" class="form-select">
                    <option value="todas">Todas as tarefas</option>
                    <option value="pendentes">Tarefas Pendentes</option>
                    <option value="finalizadas">Tarefas finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>