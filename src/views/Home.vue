<template>
  <div class="home">
    <div class="logo-header">
      <img src="../assets/ESS.png">
      <img src="../assets/ministrstvo-logo.png">
    </div>
    <img src="../assets/logo.png">
    <h1>Dragi igralec_ka,</h1>
    <p>
      Organizacije civilne družbe preko zagovorniških dejavnosti spreminjajo družbo na bolje in s
      svojimi storitvami vskočijo tam, kjer državnim institucijam zmanjka kapacitet ali pa volje za
      reševanje problematike. Trenutno se spopadajo z obsežnimi kritikami splošne publike, večkrat
      pa celo s strani vlade in nekaterih medijev. Velikokrat se celoten sektor organizacij civilne
      družbe označuje za zajedalca državnega proračuna, posamezne organizacije pa tudi za zaviralke
      “razvoja”.
      <br />
      <br />
      Vabljen_a si, da s pomočjo naše kratke interaktivne igrice malo bolje spoznaš delovanje
      organizacij civilne družbe in njihovo vlogo pri razvoju družbe.
    </p>
    <router-link v-if="wideEnough" to="/game" class="button">ZAČNI IGRO!</router-link>
    <h1 v-else>Igro lahko igraš samo na velikih zaslonih s tipkovnico. :(</h1>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import HelloWorld from '@/components/HelloWorld.vue'; // @ is an alias to /src

@Component({
  components: {
    HelloWorld,
  },
})
export default class Home extends Vue {
  private wideEnough: boolean;

  constructor() {
    super();
    this.wideEnough = window.innerWidth > 1100;
  }
}
</script>

<style lang="scss">
@media (max-width: 1100px) {
  p {
    padding-left: 10px;
    padding-right: 10px;
  }
}
</style>
