<script setup>
const props = defineProps(['tarefasPendentes'])

console.log(props.tarefasPendentes);

</script>

<template>
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
        <h1>Minhas Tarefas</h1>
        <p v-if="props.tarefasPendentes > 0">
            Você possui {{ props.tarefasPendentes }} tarefas pendentes
        </p>
        <p v-else class="pendente">
            Oba, Nenhuma Tarefa pendente
        </p>
    </header>
</template>

<style scoped>
.pendente{
    color: red;
    font-size: 24px;
}

</style>