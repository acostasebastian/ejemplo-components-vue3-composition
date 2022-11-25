<script setup>
//defineProps(["title", "id", "body"]) //a defineProps le pasamos los valores que vamos a utilizar

//const props = defineProps(["title", "id", "body","colorText"]) 
//console.log(props.title) --definiendo los props como constantes, podemos luego ReUtilizarlos, en este caso en un console

//TAMBIEN PODEMOS PASAR LOS PROPS COMO OBJETOS
defineProps({
    title: String,
    id: Number,
    body: {
        type: String,
        default:"Sin descripción"
    }
})

const emitSeba = defineEmits(['cambiarFavoritoNombre'])
</script>

<template>
    <div class="card">
    <div class="card-body"> <!--de esta forma es como se puede traer un Prop y asignarselo a la clase text de Boostrap -->       <!-- <h5 class="card-title":class="`text-${colorText}`"> -->
        <h5 class="card-title">{{id}} - {{title}}</h5>
        <p>{{body}}</p>
        <!-- <button @click="$emit('cambiarFavoritoNombre', title)" CON EL $ SE ACCEDE A LOS EMITS GLOBALES, LOS QUE VIENEN POR DEFECTO. SINO LLEVA EL $ ES EL NOMBRE QUE PONGAMOS -->
        <button @click="emitSeba('cambiarFavoritoNombre', title)"
        class="btn btn-outline-primary">Favorito</button>
    </div>
</div>
</template>