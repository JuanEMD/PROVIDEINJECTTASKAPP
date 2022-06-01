<template>
  <div class="alert alert-warning mt-3 d-flex justify-content-between align-items-center">
    <p class="m-0" :class="{'tachado': tarea.estado}"> {{tarea.texto}} </p>
    <div>
        <i class="fa-solid fa-undo-alt mx-2 text-success" role="button" @click="modificar(tarea.id)" v-if="tarea.estado"></i>
        <i class="fa-solid fa-circle-check mx-2 text-success" role="button" @click="modificar(tarea.id)" v-else></i>
        <i class="fa-solid fa-circle-minus text-danger" role="button" @click="eliminar(tarea.id)"></i>
    </div>
  </div>
</template>

<script setup>
import { inject } from 'vue';

    const props = defineProps({
        tarea: {
            type: Object,
            required: true,
        }
    })

    const tareas = inject('tareas')

    const eliminar = id => {
        tareas.value = tareas.value.filter(item => item.id !== id)
    }
    const modificar = id => {
        tareas.value = tareas.value.map(item => {
            if(item.id == id){
                item.estado = !item.estado
            }
            return item
        })
    }
</script>

<style scoped>
    .tachado{
        text-decoration: line-through
    }
</style>