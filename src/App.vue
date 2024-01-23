<script setup>

  const name = 'Vue dinámico'
  const blueStyle = 'color: blue'
  const active = false
  const show = true

  const fruitsArray = [
    {
      name: "Manzana",
      price: "$1.00",
      description: "Una manzana",
      stock: 0,
    },
    {
      name: "Pera",
      price: "$2.00",
      description: "Una pera",
      stock: 10,
    },
    {
      name: "Naranja",
      price: "$3.00",
      description: "Una naranja",
      stock: 5,
    },
  ];

  const fruitsObject = {
    name: "Manzana",
    price: "$1.00",
    description: "Una manzana",
  };

  const users = [
  {
    id: 1,
    name: 'Juan',
    posts: [
      { id: 1, title: 'Mi primer post' },
      { id: 2, title: 'Mi segundo post' },
    ]
  },
  {
    id: 2,
    name: 'Maria',
    posts: [
      { id: 3, title: 'Mi tercer post' },
      { id: 4, title: 'Mi cuarto post' },
    ]
  }
];

//imports
import {ref, computed} from 'vue'
 
const handleclick = (msg) => {
  console.log(msg);
};

const num = ref(0)
const incrementNum = () => num.value ++;
const decresetNum = () => num.value --;
const resetNum = () => (num.value = 0);

const classNum = computed(() => {
  if(num.value === 0){
    return 'zero'
  }
  if(num.value < 0){
    return 'negative'
  }
  if(num.value > 0){
    return 'positive'
  }
})

</script>

<template>
  <h1> {{ name.toLocaleUpperCase() }} </h1>
  <h2 :style="blueStyle"> Blue title </h2>
   
  <p v-if="active"> active parragraph </p>
  <p v-else-if="active === false"> inactive parragraph </p>
  <p v-else> ??? </p>

  <h2 v-show="show">Show function</h2>

  <h3>V-FOR: ARRAYS</h3>
  <ul>
    <li 
    v-for="(fruit, i) in fruitsArray"
    :key="fruit.name"
    >
      {{ fruit.name }} - {{ fruit.price }} - {{ fruit.description }}
    </li>
  </ul>
  <hr>
  <h3>V-FOR: OBJECTS</h3>
  <ul>
    <li
    v-for="(value, property, i) in fruitsObject"
    :key="value"
    >
    {{ i }} - {{ property }}: {{ value }}
    </li>
  </ul>
  <hr>
  <h3>V-FOR + V-IF</h3>
  <ul>
    <template v-for="(fruit, i) in fruitsArray" :key="i" >
      <li v-if="fruit.stock > 0">
      {{ fruit.name }} - {{ fruit.price }} - {{ fruit.description }} ({{ fruit.stock }})
      </li>
    </template>
  </ul>

  <div>
    <h2>Lista de usuarios:</h2>
    <ul>
      <template v-for="(user, index) in users" :key="user.id">
        <li>
          <h3>{{ user.name }}</h3>
          <ul>
            <template v-for="(post, index) in user.posts" :key="post.id">
              <li>{{ post.title }}</li>
            </template>
          </ul>
        </li>
      </template>
    </ul>
  </div>

  <hr>
  <h3>V-ON</h3>
  <button @click="handleclick('click')" >Click</button>

  <hr>
  <h3>V-ON + REF (SEGUIR VARIABLE QUE PUEDE CAMBIAR)</h3>
  <button @click="incrementNum('click')">+</button>
  <button @click="decresetNum('click')">-</button>
  <button @click="resetNum('click')">reset</button>

  <h4 :class="classNum">{{ num }}</h4>
  


</template>
// v-bind:style="" === : --> me permite darle estilo a los atributos con variables guardadas, tiene el mismo efecto que las {{ }}
// v-if - v-else-if - v-else --> muestro algo dependiendo de la condición
// v-show --> muestro algo o no dependiendo de su condición
// v-for --> indicar un key distintivo a cada elemento (recomendable)

// V-IF TIENE MÁS PRIORIDAD QUE V-FOR - si quiero usarlos juntos, tengo que hacer el v-if dentro del v-for (que no es lo más recomendado) ó usar otro template dentro.
// v-on="" === : @



<style>
h1 {
  color: brown;
}

.positive {
  color: green;
}

.negative {
  color: red;
}

.zero {
  color: black;
}
</style>