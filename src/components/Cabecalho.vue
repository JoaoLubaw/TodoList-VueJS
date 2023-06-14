<script setup>
    const props = defineProps(['tarefasPendentes'])
</script>


<template>
    <header class="p-5 mb-4 mt-4 bg-light rouded-3">
        <h1>Minhas tarefas</h1>
        <p>Você possuí {{ props.tarefasPendentes }} tarefas pendente</p>
    </header>
</template>  

<style>
</style>