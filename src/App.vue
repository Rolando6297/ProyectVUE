<script setup>
  const name = "Vue Dinamico";
  const color1 = "color: blue";
  const arrayColor = ["blue", "red", "yellow", "peru"];
  const activo = true;
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


</template>

<style>
h1{
  color: red;
}
</style>