<script setup>
    const props = defineProps(['tarefas']);
</script>

<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefas">
            <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada"
                :id="tarefa.titulo" type="checkbox">
            <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
    <ul class="list-group mt-4">
    <transition name="fade">
        <li class="list-group-item" v-if="props.tarefas.filter(t => !t.finalizada).length === 0">
            Não existem tarefas pendentes
        </li>
    </transition>
</ul>
</template> 
<style scoped>
    .fade-enter-active, .fade-leave-active {
    transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active em versões <2.1.8 */ {
    opacity: 0;
}


    .done {
        text-decoration: line-through;
    }
</style>