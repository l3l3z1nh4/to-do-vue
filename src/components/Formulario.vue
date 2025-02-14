<script setup>
    const props = defineProps(['cadastraTarefa', 'tarefaTemp', 'trocarFiltro','editaTarefaTemp'])
</script>


<template>
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row">
            <div class="col">
                <input :value="props.tarefaTemp"  @change=" props.editaTarefaTemp" required type="text" placeholder="adicionar tarefa" class="form-control">
            </div>
        <div class="col-md-1">
        <button type="submit" class="btn btn-primary">+</button>
        </div>
        <div class="col-md-2">
        <select @change=" props.trocarFiltro" class="form-control">
            <option value="todas">Todas as tarefas</option>
            <option value="pendentes">Tarefas pendentes</option>
            <option value="concluidas">Tarefas concluidas</option>
        </select>
        </div>
        </div> 
    </form>
</template>