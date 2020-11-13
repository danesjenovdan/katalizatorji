<template>
  <div class="home">
    <div class="logo-header">
      <img src="../assets/ESS.png">
      <img src="../assets/ministrstvo-logo.png">
    </div>
    <img src="../assets/logo.png">
    <h1>Igre je konec!</h1>
    <p>
      Košara organizacij civilne družbe je zapolnjena. Organizacijam civilne družbe primanjkuje
      sredstev in kadrovske moči za vse potrebe, ki jih naslavljajo. Trenutno žal zato ne morejo
      zagotoviti vsega, kar naša družba potrebuje.
      <br />
      <br />
      Vse to se lahko spremeni tudi s tvoji podporo! Sprememba je edina konstanta in tudi ti lahko
      igraš vlogo v spreminjanju našega političnega, ekonomskega in socialnega sistema.
    </p>
    <router-link to="/game" class="button">Poskusi znova</router-link>
    <router-link to="/support" class="button support">Podpri sektor civilne družbe!</router-link>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

@Component
export default class GameOver extends Vue {}
</script>
