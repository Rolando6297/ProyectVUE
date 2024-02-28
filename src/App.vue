<script setup>
  const name = "Vue Dinamico";
  const color1 = "color: blue";
  const arrayColor = ["blue", "red", "yellow", "peru"]
  const activo = false
</script>

<template>
  <h1>{{ name }} de Rolando </h1>              <!-- // uso de llaves para constante en texto -->
  <h2 v-bind:style="color1">Soy azul</h2>       <!-- // uso de constantes para atributos -->
  <h2 :style="color1">Soy azul abreviado</h2>       <!-- // uso de constantes para atributos abreviado -->
  <h1>{{ name.toUpperCase() }} de Rolando </h1>              <!-- // funciones dentro de llaves de bigotes -->
  <h3>{{ arrayColor }}</h3>
  <h3 :style="`color: ${arrayColor[3]}`">{{ arrayColor }}</h3>  <!-- color de array uso de comillas invertidas y llave sencilla dentro para poner color -->
  <h4> {{ activo ? "estoy activo" : "estoy inactivo" }}</h4>    <!--estadp condicio directa de vue (if) de variable activo-->
  <p v-if="!activo"> estoy activo :l
  git 
  </p>

</template>

<style>
h1{
  color: red;
}
</style>