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
    <router-link to="/" class="button share">DELI S PRIJATELJI</router-link>
    <router-link to="/" class="button support">NAMENI DOHODNINO</router-link>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

@Component
export default class Support extends Vue {}
</script>
