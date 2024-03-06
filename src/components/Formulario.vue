<script setup>
    const props = defineProps(['cadastraTarefa', 'tarefaTemp', 'trocarFiltro', 'editaTarefaTemp'])
</script>
<template>
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row">
            <div class="col">
                <input :value="props.tarefaTemp" @change="props.editaTarefaTemp" required type="text" placeholder="Digite a descrição da tarefa" class="form-control">
            </div>
            <div class="col-md-2">
                <button class="btn btn-primary" type="submit">Cadastra</button>
            </div>
            <div class="col-md-2">
                <select @change="props.trocarFiltro" class="form-control">
                    <option value="Todas">Todas tarefas</option>
                    <option value="Pendentes">Pendentes</option>
                    <option value="Finalizadas">Finalizada</option>
                </select>
            </div>
        </div>
    </form>
</template>