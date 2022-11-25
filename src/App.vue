<script setup>
import {onMounted, ref} from "vue";                                                      

import BlogPost from './components/BlogPost.vue';
import PaginatePost from './components/PaginatePost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';

import ButtonCounter from './components/ButtonCounter.vue' // esto es para traerme el componente creado en la carpeta components, del tipo .vue. El primer ButtonCounter es el nombre, 
                                                       // pero se recomienda nombrarlo igual al componente a traer. Y luego lo uso en el template como cualquier etiqueta HTML

//array de Objetos para recorrer
// const posts = ref([
//   {title: 'Post 1', id: 1, body: 'descripcion 1'},
//   {title: 'Post 2', id: 2, body: 'descripcion 2'},
//   {title: 'Post 3', id: 3, body: 'descripcion 3'},
//   {title: 'Post 4', id: 4},
// ]) 

//array dinamico que se cargara con la URL de json
const posts = ref([])

//Paginación 
const postXpage = 10 //cantidad de elementos por página
const inicio = ref(0)
const fin = ref(postXpage)
const loading = ref(true)

const favorito = ref("");
const cambiarFavorito = (title) => {
    favorito.value = title;
}


const next =() => {
  inicio.value = inicio.value + postXpage
  fin.value = fin.value + postXpage
}

const prev =() => {
  //inicio.value = inicio.value - postXpage
  inicio.value +=  - postXpage
  fin.value = fin.value - postXpage
}


// onMounted(   () => {
//       fetchData();
// })

//URL DE DONDE TRAER DATOS JSON. 
//como los datos consumidos de la api y los nuestros (en BlogPost) tienen el mismo nombre (title, id,body), se les puede pasar directamente desde el data sin tener que asignarlos
// fetch('https://jsonplaceholder.typicode.com/posts')
// .then((res) => res.json())
// .then((data) => {
//   posts.value = data;
// })
// .catch((e) => console.log(e))
// .finally(() => loading.value = false)

//FORMA MAS EFICIENTE YA QUE SE USA ASYNC
const fetchData = async() => {
  
  try {
      const res = await fetch("https://jsonplaceholder.typicode.com/posts") 
      posts.value = await res.json() ;
  } catch (error) {
    console.log(error)
  } finally{
    setTimeout(() => {
      loading.value = false;
    },2000);
  }
};

fetchData()

</script>

<template>
<LoadingSpinner v-if="loading"/>

  <div class="container" v-else>
    <h1>APP</h1>
  <!-- <ButtonCounter>  </ButtonCounter> -->
  <!-- <BlogPost title="Post 1" id="1" body="Descripcion 1" colorText="primary"/> -->
  <!--<BlogPost title="Post 1" :id="1" body="Descripcion 1"/>   se le pone :id para que lo tome como numero, que es el tipo definido -->
  <h2> Mi post Favorito: {{favorito}}</h2>
  <PaginatePost @next="next" @prev="prev" :inicio="inicio" :fin="fin" :maxLength = "posts.length"  class="mb-2"/>  <!-- envio los metodos creados al componente PaginatePost -->
  <BlogPost 
    v-for="post in posts.slice(inicio,fin)" 
    :key="post.id"  
    :title="post.title" 
    :id="post.id" 
    :body="post.body"
    @cambiarFavoritoNombre="cambiarFavorito"
    class="mb-2"
  ></BlogPost> 

  </div>
  
</template>