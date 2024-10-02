<script setup>
const props = defineProps(['cadastrarTarefa', 'tarefaTemp', 'trocarFiltro','editaTarefaTemp'])

</script>

<template>
    <form @submit.prevent="cadastrarTarefa">
        <div class="row">
            <div class="col">
                <input :value="tarefaTemp" @change="editaTarefaTemp" required
                    type="text" placeholder="Digite aqui a tarefa" class="form-control">
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-3">
                <select @change="trocarFiltro" class="form-control">
                    <option value="todas">Todas as tarefas</option>
                    <option value="pendentes">Tarefas pendentes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template> 
