<script setup>
import { onMounted, ref } from 'vue';
import { useRoute } from 'vue-router';
const route=useRoute()
let movie=ref({})
onMounted(async ()=>{
    const res = await fetch(`http://www.omdbapi.com/?apikey=${''}&i=${route.params.id}`)
    .then(response => response.json())
    movie.value = res;
    console.log(res);
})
</script>
<template>
    <div v-if="movie.Title" class="movie-detail">
      <h2>{{movie.Title}}</h2>
      <p>{{ movie.Year }}</p>
      <img :src="movie.Poster" alt="Movie Poster" class="featured-img" />
      <p>{{ movie.Plot }}</p>
    </div>
    <div v-else class="movie-detail" style="color: #fff;">
        LOADING ....
    </div>
  </template>
  
  <style lang="scss">
.movie-detail {
  padding: 16px;
  h2 {
    color: #FFF;
    font-size: 28px;
    font-weight: 600;
    margin-bottom: 16px;
  }
  .featured-img {
    display: block;
    max-width: 200px;
    margin-bottom: 16px;
  }
  p {
    color: #FFF;
    font-size: 18px;
    line-height: 1.4;
  }
}
</style>