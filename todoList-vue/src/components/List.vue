<script setup>
    const props = defineProps(['tarefas', 'delete'])
</script>

<template>
    <ul v-if=" props.tarefas.length != 0" class="list-group mt-4">
        <li v-for="tarefas in props.tarefas" class="list-group-item d-flex  align-items-center">
            <input @change="evento => tarefas.finish = evento.target.checked" :checked="tarefas.finish" :id="tarefas.title"
                type="checkbox">
            <label :class="{ done: tarefas.finish }" class="ms-3 flex-grow-1" :for="tarefas.title">
                {{ tarefas.title }}
            </label>
            <a @click="props.delete(tarefas.title)" class="text-danger cursor-pointer">Deletar</a>
        </li>
    </ul>
    <h4 v-else class="mt-3">Nenhuma tarefa</h4>
</template>

<style scoped>
    .done{
    text-decoration: line-through;
    }
    .cursor-pointer{
        cursor: pointer;
    }
</style>
