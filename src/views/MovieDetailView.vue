<template>
  <div class="details">
    <div class="movieCtn" :style="{ backgroundImage: `url(${movie.image})` }">
      <div class="title">
  
        <div class="">{{ movie.title }}</div>
      </div>
    </div>
    <star-rating
    :rating="movie.rank"
    star-size="20"
    increment="0.5"
    :show-rating="false"
    class="star"
  />
    <p>description:</p>
    <div class="description">{{ movie.description }}</div>
    
  </div>
</template>

<script setup>
import { reactive, onMounted } from 'vue';
import { useRoute } from 'vue-router';
import StarRating from 'vue-star-rating';
const route = useRoute();
const movieId = route.params.id;

const movie = reactive({});

onMounted(() => {
  fetchDetailMovie()
});

const fetchDetailMovie = () => {
  fetch('datas/details/movies.json')
    .then(response => response.json())
    .then(data => {
      const foundMovie = data.movies.find(m => m.id === parseInt(movieId));
      if (foundMovie) {
        movie.title = foundMovie.title;
        movie.image = foundMovie.image;
        movie.rank = foundMovie.rank;
        movie.description = foundMovie.description;
        movie.trailer = foundMovie.trailer
      }
    })
    .catch(error => console.error('Erreur lors du chargement du JSON:', error));
}
</script>

<style scoped lang="scss">
.details {
  .title {
    position: relative;
    text-align: center;
    display: flex;
    justify-content: space-between;
    padding: 15% 0 0 15%;
  
    font-size: 25px;
    z-index: 40;
   
  }

  .star{
    display: flex;
    justify-content: center;
    padding: 20px;
  }
  .rounded {
    text-align: end;
    padding: 5px 20px;
  }

  .description{
    font-size: 20px;
    
  }
  .movieCtn {
    height: 40vh;
    background-size: cover;
    background-position: center;
    position: relative;
  }

  .movieCtn::after {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    height: 40%;
    z-index: 1;
    width: 100%;
    background: linear-gradient(0deg, rgba(2, 0, 36, 0) 0%, rgba(0, 0, 0, .7) 100%);
  }
}
</style>
