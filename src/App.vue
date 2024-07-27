<script setup>
import { ref, computed } from 'vue';

const counter = ref(0)
const arrayFavorite = ref([])

const increment = () => counter.value++
const decrement = () => counter.value--
const restart = () => {
  counter.value = 0;
  arrayFavorite.value = []
}
const add = () => arrayFavorite.value.push(counter.value)


const classCounter = () => {
  if (counter.value === 0) {
    return 'zero';
  }
  if (counter.value < 0) {
    return 'negative'
  }
  if (counter.value > 0) {
    return 'positive'
  }
};
const bloquearBtnAdd = computed(() => {
  const numSearch = arrayFavorite.value.find(num => num === counter.value)
  if (numSearch === 0) return true
  return numSearch ? true : false;
})
</script>


<template>
<div class="container text-center -5">
  <h1> Contador </h1>
  <h2 :class=classCounter()>{{ counter }}</h2>
  <br>
  <div class="btn-group">
    <button @click="increment" class="btn btn-success">Aumentar</button>
    <button @click="decrement" class="btn btn-danger">Disminuir</button>
    <button @click="add" class="btn btn-primary" :disabled='bloquearBtnAdd'>Agregar</button>
    <button @click='restart' class="btn btn-secondary">Reiniciar</button>
  </div>
  <ul class="list-group mt-4">
    <li class="list-group-item" v-for="(num, index) in arrayFavorite" :key="index">{{ num }}</li>
  </ul>
</div>
</template>


<style>
h1 {
  color: red;
}

.positive {
  color: green
}

.negative {
  color: red
}

.zero {
  color: peru
}
</style>