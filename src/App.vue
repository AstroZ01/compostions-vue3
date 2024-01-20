<script setup>
import { computed } from "@vue/reactivity";
import {ref, onUnmounted, onMounted} from 'vue';
import ButtonCounter from './components/ButtonCounter.vue';
import BlogPost from './components/BlogPost.vue';
import PaginatePost from './components/PaginatePost.vue';
import SpinnerMid from './components/SpinnerMid.vue';

const posts = ref([]);
const postsXpage = 10;
const inicio = ref(0);
const fin = ref(postsXpage);
const loading =ref(true);

  const favorito = ref('')

  const cambiarFavorito = (title) => {
    favorito.value = title
  };

  const next = () => {
    inicio.value =  inicio.value + postsXpage
    fin.value = fin.value + postsXpage
  }

  const prev = () => {
    inicio.value = inicio.value - postsXpage
    fin.value = fin.value - postsXpage
  }

  // onMounted  (async() => {
  //   loading.value = true;
  //   try{
  //   const res =  await fetch ("https://jsonplaceholder.typicode.com/posts");
  //   posts.value = await res.json();
  // } catch(error){
  //     console.log(error);
  //   } finally{
  //     loading.value = false;
  //   }

  // });
  // fetch ('https://jsonplaceholder.typicode.com/posts')
  // .then(res => res.json())
  // .then(data => {
  //   posts.value = data;
  // })
  // .catch((e) => console.log(e))
  // .finally(( ) => {
  //   setTimeout(() => {
  //     loading.value = false
  //   }, 2000);
  // });

  const fetchData = async () => {
    try{
     const res =  await fetch ("https://jsonplaceholder.typicode.com/posts");
     posts.value = await res.json();
   } catch(error){
      console.log(error);
    } finally{
      loading.value = false;
  }
  }

  fetchData();


  const maxLength = computed(() => posts.value.length);

</script> 



<template>
  <SpinnerMid v-if="loading"/>
  <div class="container" v-else>
    <h1>APP</h1>
    <h2>Mis posts favorito: {{ favorito }}</h2>

    <paginatePost class="mb-2"
    @next="next" 
    @prev="prev"
    :inicio="inicio"
    :fin="fin"
    :maxLength="maxLength">
  </paginatePost>

 <BlogPost v-for="pop in posts.slice(inicio,fin)"
            :key="pop.title"
            :title="pop.title"
            :id="pop.id"
            :body="pop.body"
            :cambiarFavorito="cambiarFavorito"
            class="mb-2"/>
            
</div>
 </template>