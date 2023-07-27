<template>
  <div class="app">
    <h2>Vue 3 Counter</h2>

    <div :class="classCounter">{{ counter }}</div>

    <div class="btn-action">
      <button @click="increment">Increment</button>
      <button @click="decrement">Decrement</button>
      <button @click="reset" :disabled="counter === 0">Reset</button>
      <button @click="addFavorite" :disabled="blockIsAdded">
        Add Favorite
      </button>
    </div>

    <label for="">{{ favorites.length > 0 ? "Favorite List" : "" }}</label>
    <ul>
      <li v-for="(value, i) in favorites" :key="i">
        {{ value }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const counter = ref(0);

const favorites = ref([]);

const addFavorite = () => {
  favorites.value.push(counter.value);
};

const blockIsAdded = computed(() => {
  const numberSearch = favorites.value.find((item) => item === counter.value);
  return numberSearch || numberSearch === 0;
});

const increment = () => {
  counter.value++;
};

const decrement = () => {
  counter.value--;
};

const reset = () => {
  counter.value = 0;
  favorites.value = [];
};

const classCounter = computed(() => {
  if (counter.value === 0) {
    return "zero";
  }
  return counter.value > 0 ? "positive" : "negative";
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.negative {
  color: red;
}
.positive {
  color: green;
}
.zero {
  color: orange;
}

ul {
  list-style: none;
  padding: 0;
}
li {
  background: #ccc;
}

.btn-action {
  margin-top: 4px;
}
</style>
