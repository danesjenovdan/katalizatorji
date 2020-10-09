<template>
  <div class="home">
    <img src="../assets/logo.png">
    <h1>Igre je konec</h1>
    <p>
      Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt
      ut labore et dolore magna aliqua. Quis ipsum suspendisse ultrices gravida. Risus commodo
      viverra maecenas accumsan lacus vel facilisis.
      <br />
      <br />
      Quis ipsum suspendisse ultrices gravida. Risus commodo viverra maecenas accumsan lacus
      vel facilisis.
    </p>
    <router-link to="/game" class="button">Poskusi znova</router-link>
    <router-link to="/support" class="button support">PODPRI CIVILNO DRUŽBO</router-link>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

@Component
export default class GameOver extends Vue {}
</script>
