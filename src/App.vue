<template>
  <h1>Hola Vue JS {{ name.toUpperCase() }}</h1>
  <h2>{{ arrayColores }}</h2>
  <h2 :style="styleColor">Soy azul</h2>
  <h2 :style="`color: ${arrayColores[0]}`">Otro azul</h2>
  <h2>{{ activo ? "Estoy activo" : "Estoy inactivo" }}</h2>
  <p v-if="activo">Estoy aqui</p>
  <p v-else>No hay nada</p>

  <span v-if="numero === 1">Uno</span>
  <span v-else-if="numero === 2">Dos</span>
  <span v-else>{{ numero }}</span>

  <br />

  <ul>
    <li v-for="(fruta, index) in arrayFrutas"
        :key="index">
      {{ index }} - {{ fruta }}</li>
  </ul>

  <br />

  <ul>
    <li v-for="item in arrayFrutas2" :key="item.id">
      {{ item.name }} -{{ item.price }} - {{ item.description }}
    </li>
  </ul>

  <br />

  <ul>
    <li v-for="(value, propiedad, index) in fruta" :key="index">
      {{ index }} - {{ propiedad }} : {{ value }}
    </li>
  </ul>

  <br />

  <ul>
    <li v-for="item in arrayFrutas3" :key="name">
      <span v-if="item.stock > 0">
        {{ item.name }} - {{ item.price }}
      </span>
    </li>
  </ul>

  <br />

  <ul>
    <template v-for="item in arrayFrutas3" :key="name">
      <li v-if="item.stock > 0">
        {{ item.name }} - {{ item.price }}
      </li>
    </template>
  </ul>

  <br />

  <button @click="handleClick('clickeado')">Activame</button>
  <button @click.right.prevent="handleClick('right')">Right click me</button>
  <button @click.left="handleClick('left')">Left click me</button>
  <button @click.middle="handleClick('middle')">Middle click me</button>

  <br />
  <h2 :class="{ 'app-alert': counter < 0, 'app-ok': counter > 0 }">{{ counter }}</h2>
  <button @click="increment">Aumentar</button>
  <br />
  <button @click="decrement">Decrementar</button>
  <br />
  <button @click="resetCounter">Reset contador</button>

  <br />  
  <br />
  <br />

  <h2 :class="classCounter">{{ counter }}</h2>
  <button @click="increment">Increment</button>
  <button @click="decrement">Decrement</button>
  <button @click="resetCounter">Reset</button>
  
  <br />  
  <br />
  <br />

  <span>Employee name: {{ employeeName }}</span>
  <br />
  <input type="text" v-model="employeeName">
  <br />
  <button @click="setEmployeeName('')">Clear Name</button>

  <br />  
  <br />
  <br />

  <ul>
    <li v-for="(number, index) in arrayFavoriteNumber" :key="index">
      {{ number }}
    </li>
  </ul>
  <span>Insert your favorite number:</span>
  <br />
  <input type="text" v-model="favoriteNumber" placeholder="Insert your favorite number">
  <br />
  <button @click="appendFavoriteNumber" :disabled="!canInsertNumber()">Append</button>
</template>

<style>
.zero {
  color: black;
}

.app-alert, .negative {
  color: red;
}

.app-ok, .positive {
  color: green;
}
</style>

<script setup>

import { ref, computed } from 'vue';

const arrayFavoriteNumber = ref([]);
const favoriteNumber = ref(0);

const canInsertNumber = () => {
  return !isNaN(favoriteNumber.value) && !arrayFavoriteNumber.value.includes(favoriteNumber.value);
}

// pushes a new favorite number, it can not allow repeated values neither NaN values
const appendFavoriteNumber = () => {
  if (canInsertNumber()) {
    arrayFavoriteNumber.value = [...arrayFavoriteNumber.value, favoriteNumber.value];
  }
}

const name = "Vue dinamico";
const styleColor = "color: blue";
const arrayColores = ["blue","red","peru"]
const activo = false;
const numero = 10;
const arrayFrutas = ["manzana","platano","sandia","fresa","cereza"];
const arrayFrutas2 = [
  {
    id: 1,
    name: "Manzana",
    price: "$1.00",
    description: "Una manzana"
  },
  {
    id: 2,
    name: "Pera",
    price: "$2.00",
    description: "Una pera"
  },
  {
    id: 3,
    name: "Naranja",
    price: "$3.00",
    description: "Una naranja"
  }
];
const fruta = {
  id: 1,
  name: "Manzana",
  price: "$1.00",
  description: "Una manzana"
};
const arrayFrutas3 = [
  {
    name: "Manzana",
    price: "$1.00",
    description: "Una manzana",
    stock: 0
  },
  {
    name: "Pera",
    price: "$2.00",
    description: "Una pera",
    stock: 10
  },
  {
    name: "Naranja",
    price: "$3.00",
    description: "Una naranja",
    stock: 20
  }
];

const counter = ref(0);
const employeeName = ref("Unnamed");

const handleClick = (message) => {
  console.log(message);
}

const increment = () => {
  counter.value++;
}

const decrement = () => {
  counter.value--;
  if (counter.value < 0) {

  }
}

const resetCounter = () => {
  counter.value = 0;
}

const setEmployeeName = (name) => {
  employeeName.value = name;
}

const classCounter = computed(() => {
  if (counter.value === 0) {
    return "zero";
  }
  if (counter.value > 0) {
    return "positive";
  }
  if (counter.value < 0) {
    return "negative";
  }
});
</script>