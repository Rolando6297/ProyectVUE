<script setup>
import {ref, computed} from "vue"
  const name = "Vue Dinamico";
  const color1 = "color: blue";
  const arrayColor = ["blue", "red", "yellow", "peru"];
  const activo = true;
  const arrayFrutas = ["🍎", "🍌", "🍉", "🍓", "🍒"];
  const arrayFrutas2 = [
        {
            name: "Manzana",
            price: "$1.00",
            description: "Una manzana",
        },
        {
            name: "Pera",
            price: "$2.00",
            description: "Una pera",
        },
        {
            name: "Naranja",
            price: "$3.00",
            description: "Una naranja",
        },
    ];
    const objetoFruta = {
            name: "Naranja",
            price: "$3.00",
            description: "Una naranja",
    };
    const arrayFrutas3 = [
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
        stock: 20,
    },
];
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

const  counter = ref(0); //variable reactiva
// class computer para formato condicional
const classCounter = computed(()=>{
  if (counter.value ==0){return 'zero'}
  if (counter.value < 0){return 'negative'}
  if (counter.value >0){return 'positive'}
})

const classBtn = computed(()=>{
  const  numSearch = ArrayFavorite.value.find(num=> num===counter.value)
  console.log(numSearch)
  if (numSearch ==0 )return true;
  return numSearch ? true : false ;
})

const ArrayFavorite = ref([]);
//<!--metodo-->
const AddFavorite = (numero)=>{ ArrayFavorite.value.push(numero)
console.log(ArrayFavorite)}
const handleclick = () => {console.log("me dieron click")};
const handleclickn = (nombre) => {console.log("me dieron click " + nombre)};
const increment = () =>{
  counter.value ++  //ractiva
  console.log(counter)
  
}
const decrement = () =>{
  counter.value --  //ractiva

}
const reset = () =>{
  counter.value = 0  //ractiva

}
</script>

<template>
  <h1>{{ name }} de Rolando </h1>              <!-- // uso de llaves para constante en texto -->
  <h2 v-bind:style="color1">Soy azul</h2>       <!-- // uso de constantes para atributos -->
  <h2 :style="color1">Soy azul abreviado</h2>       <!-- // uso de constantes para atributos abreviado -->
  <h1>{{ name.toUpperCase() }} de Rolando </h1>              <!-- // funciones dentro de llaves de bigotes -->
  <h3>{{ arrayColor }}</h3>
  <h3 :style="`color: ${arrayColor[3]}`">{{ arrayColor }}</h3>  <!-- color de array uso de comillas invertidas y llave sencilla dentro para poner color -->
  <h4> {{ activo ? "estoy activo" : "estoy inactivo" }}</h4>    <!--estadp condicio directa de vue (if) de variable activo-->
  <p v-if="activo == false" :style="`color: ${arrayColor[1]}`"> Estoy Inactivo</p><!--if-->
  <h1 v-else-if ="activo == true" :style="`color: ${arrayColor[3]}`"> Estoy Activo</h1><!--elseif-->
  <h1 v-else :style="`color: ${arrayColor[3]}`"> Estado desconocido</h1> <!--else--->
  <h3 v-show="activo">como funcion</h3>


  <!--           ------              v-for      --------        -->


  <ul>
    <li v-for="fruta , index in arrayFrutas" :key="index"> {{ index }} {{ fruta }} </li> <!--key es para distinguir con un parametro unico-->
  </ul>  <!--fruta o index pueden tener cualquier nombre, solo el primero es el elemento y el seundo es el numero-->

  <ul>
    <li v-for="fruta , index in arrayFrutas2" :key="fruta.name">  {{ fruta }} </li> <!--key es para distinguir con un parametro unico-->
  </ul>  <!--fruta o index pueden tener cualquier nombre, solo el primero es el elemento y el seundo es el numero-->
<div style="color: blue"> {{ objetoFruta }}</div>
 <!--   --------  for en objetos -------   -->
<div>
  <ul>
    <li v-for="elemento , clave, index in objetoFruta" :key="elemento">
      {{ clave }} : {{ elemento  }} , {{ index }}

    </li>
  </ul>
</div>

  <!--          uso de v for y v if           -->

  <ul>
    <!-- <li v-for="fruta in arrayFrutas3" :key="fruta.name" v-if="fruta.stock > 0">  tiene prioridad el if que el vfor
     <li v-for="fruta in arrayFrutas3" :key="fruta.name" >
    <p v-if="fruta.stock > 0">     se soluciona creando nueva etiqueta añidada
      {{ fruta.name }}  -  {{ fruta.price }}  --  {{ fruta.stock }}
    </p>
    </li>
    -->
    <template v-for="fruta in arrayFrutas3" :key="fruta.name">  <!--hara que con vfor y vif no se imprima li-->
      <li v-if="fruta.stock > 0">
        {{ fruta.name }}  -  {{ fruta.price }}  --  {{ fruta.stock }}
      </li>
    </template>
  </ul>
  <!-- for anidados-->
  <ul>
      <template
        v-for="(user, index) in users"
        :key="user.id"
      >
        <li>
          <h3>{{ user.name }}</h3>
          <ul>
            <template
              v-for="(post, index) in user.posts"
              :key="post.id"
            >
              <li>{{ post.title }}</li>
            </template>
          </ul>
        </li>
      </template>
    </ul>

<!-- v-on @ -->

    <button  v-on:click="handleclick">activame</button>
    <button @:click ="handleclickn('Rolando')">activame @</button>


    <button @:click.right ="handleclickn('rigth')">activame left</button>
    <button @:click.left ="handleclickn('left')">activame left</button>
    <button @:click.middle ="handleclickn('midle')">activame midle</button>
    <button @:click.right.prevent ="handleclickn('right')">activame midle desabilita click derecho</button>
    <button @:click.left ="increment()">Contador</button>
    <!-- reactividad o renderizado-->
    
    <h1 :class="classCounter">{{counter}}</h1>  <!--formato condicional con computed-->
    <button @:click.left ="decrement()">Disminuir</button>
    <button @:click.left ="reset()">Resetear</button>


    <div class="container text-center mt-3">
      <h1 :class="classCounter">{{counter}}</h1>  <!--formato condicional con computed-->
      <div class="btn-group" >

        <button @:click ="increment()" class="btn btn-success" >Aumentar</button>  
    <button @:click ="decrement()" class="btn btn-danger">Disminuir</button>
    <button @:click ="reset()" class="btn btn-secondary">Resetear</button>
    <button @:click ="AddFavorite(counter)" class="btn btn-primary" :disabled="classBtn">Añadir a favoritos</button>
      <br>
      </div>

    <ul class="list-group">
      <h1>Favoritos</h1>
      
      <li class="list-group-item mt-3" v-for="numero in ArrayFavorite">{{ numero }}</li>
    </ul>
    </div>
</template>

<style>
h1{
  color: red;
}
.positive{
  color : green

}
.negative{
color: red;
}
.zero{
  color: black;
}
button{
  color: wheat;
  border-radius: 2%;
  background-color: red;
}

</style>