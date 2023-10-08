<script setup>
import { ref, onMounted } from 'vue';
import BlogsPost from './components/BlogsPost.vue';
import PaginatePost from './components/PaginatePost.vue';
import LoadingComponent from './components/LoadingComponent.vue';
import TitleComponent from './components/TitleComponent.vue';
const posts = ref([]);
const postXpage = 7;
const inicio = ref(0);
const fin = ref(postXpage);
const loading = ref(true)
const favorito = ref('')
const addFavorito = (title) => {
  favorito.value = title;
}

const next = ()=>{
  inicio.value = inicio.value + postXpage;
  fin.value = fin.value + postXpage;
}

const prev = ()=>{
  inicio.value = inicio.value - postXpage;
  fin.value = fin.value - postXpage;
}

// onMounted(async()=>{
//   try {
//     const resp = await fetch('https://jsonplaceholder.typicode.com/posts');
//     posts.value = await resp.json();
    
//   } catch (error) {
//     console.log(error);
    
//   } finally{
//     setTimeout(()=>{
//       loading.value = false;
//     },800)
//   }
 
// });
//TODO: se pude realizar la petición sin el onMounted, ya que primero se realizaria la peticion y se tendria la data y despues se cargaria 
//el componente, si se requiere acceder a un elemento del DOM antes de que cargue la data, entonces si se debe utilizar el onMounted()

const getPosts = async ()=>{
  try {
    const resp = await fetch('https://jsonplaceholder.typicode.com/posts');
    posts.value = await resp.json();
    
  } catch (error) {
    console.log(error);
    
  }finally{
    setTimeout(()=> (loading.value = false), 800 );
  }

}

//Ejecuta la función de traer los posts
getPosts();

</script>

<template>
   <LoadingComponent v-if="loading"/>
  <div class="container" v-else>
   <TitleComponent/>
    <h3>Favorito: <span class="fst-italic text-success">{{ favorito }}</span></h3>
    <PaginatePost @next="next" @prev="prev" :inicio="inicio" :fin="fin" :maxLength="posts.length"/>
    <BlogsPost v-for="post of posts.slice(inicio, fin)"
      :key="post.id" :title="post.title"
      :id="post.id"
      :description="post.body" 
      @addfavorito="addFavorito"
      />
  </div>
</template>