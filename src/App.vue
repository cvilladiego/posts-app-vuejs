<script setup>
import { ref } from 'vue';
import BlogsPost from './components/BlogsPost.vue';
import PaginatePost from './components/PaginatePost.vue';
import LoadingComponent from './components/LoadingComponent.vue';
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

fetch('https://jsonplaceholder.typicode.com/posts')
.then(res => res.json())
.then((data) => {
  posts.value = data;
})
.finally(()=> {
  setTimeout(()=>{
    loading.value = false
  },800)
});

</script>

<template>
   <LoadingComponent v-if="loading"/>
  <div class="container" v-else>
    <h1>APP</h1>
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