<template>
  <div class="movieCard" @click="goToMovie(id)">
    <img :src="image" class="poster">
    <div class="title">
      <div>{{ title }}</div>
      <div>{{ score }}/5</div>
      
    </div>
    <div>
      
    </div>
  </div>
</template>

<script setup>
import { defineProps } from 'vue'
import { useRouter } from 'vue-router';

const props = defineProps({
  title: {
    type: String,
    default: ''
  },
  image: {
    type: String,
    default: '',
  },
  score : {
    type: Number,
    default: 2
  },
  id : {
    type: Number,
    default: 0
  }
})

const router = useRouter();

const goToMovie = (id) => {
  router.push(`/movie/${id}`);
};
</script>

<style scoped lang="scss">
  .movieCard {
    margin-top: 40px;
    margin-bottom:40px;

    img {
      height: 220px;
      width: 150px;
      border-radius: 6px;
    }
    .title {
      display: flex;
      justify-content: space-between;
      padding: 0 5px;
    }
  }
</style>