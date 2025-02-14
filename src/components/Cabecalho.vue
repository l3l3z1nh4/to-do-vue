<script setup>
    const props = defineProps(['tarefasPendentes'])
</script>

<template>
    <header class="p-5 mb-4 bg-light rounded-3">
        <h1>minhas tarefas</h1>
        <p>{{ props.tarefasPendentes}} pendentes</p>
    </header>
</template>