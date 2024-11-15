<template>
  <div class="slider-container">
    <div class="slider" ref="slider">
      <button v-for="(button, index) in buttons" 
      :key="index" 
       class="slider-button" 
      :style="{
        backgroundImage: `url(${button.backgroundImage})`,
        color: button.textColor
      }">
     
        <div class="button-overlay" :style="{ backgroundColor: button.backgroundColor }">
          {{ button.label }}
        </div>
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const buttons = [
  { label: '#Popular', backgroundImage: require('@/assets/the.jpg'), backgroundColor: 'rgba(255, 84, 42, 0.796)', textColor: '#FFFFFF' },
  { label: '#Coming soon', backgroundImage: require('@/assets/bbb.jpg'), backgroundColor: 'rgb(255, 203, 32, .85)', textColor: '#FFF' },
  { label: '#Watch Party', backgroundImage: require('@/assets/aaa.jpg'), backgroundColor: 'rgba(42, 100, 255, 0.796)', textColor: '#FFF' },
  { label: '#Top Rated', backgroundImage: require('@/assets/spe.jpg'), backgroundColor: 'rgba(1, 179, 16, 0.796)', textColor: '#FFF' }
];

const slider = ref(null);

const scrollLeft = () => {
  if (slider.value) {
    slider.value.scrollBy({ left: -150, behavior: 'smooth' });
  }
};

const scrollRight = () => {
  if (slider.value) {
    slider.value.scrollBy({ left: 150, behavior: 'smooth' });
  }
};
</script>

<style scoped>
.slider-container {
  padding: 0 16px;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  width: 100%;
}

.slider {
  display: flex;
  flex-wrap: nowrap;
  gap: 16px;
  padding: 0;
  overflow-x: auto;
  scroll-behavior: smooth;
  margin: 0;
  width: 400%;
  position: relative;
}

a {
  color: rgb(255, 203, 32);
}

.slider-button {
  background-size: cover;
  min-width: 150px !important;
  height: 90px;
  border: none;
  font-size: 16px;
  border-radius: 5px;
  cursor: pointer;
  white-space: nowrap;
  position: relative;
  box-sizing: border-box;
}

.button-overlay {
  content: "";
  border-radius: 5px;
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  font-weight: 900;
  font-size: 16px;
}
</style>
