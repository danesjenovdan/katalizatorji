<template>
  <div class="home">
    <img src="../assets/logo.png">
    <h1></h1>
    <p>
      Za uspešno delovanje organizacij civilne družbe je pomembno, da niso odvisne ne od trga in ne
      od volje političnih strank. Le takšna avtonomija jim namreč lahko zagotovi, da se lahko
      resnično posvetijo svojemu delu in se ne podredijo aktualni politični oblasti ali zakonom
      prostega trga. To pa lahko dosežejo le z zadostnim in stalnim financiranjem, ki jim omogoča
      dolgoročno zaposlovanje ljudi in razvoj kadrov. A prav to je ena izmed ključnih težav
      slovenskega civilnega sektorja.
      <br />
      <br />
      Nevladne organizacije, ki tvorijo pomemben del sektorja organizacij civilne družbe,
      zaposlujejo le 0,84 % aktivnega prebivalstva. Za primerjavo, leta 2013 je ta delež v svetovnem
      povprečju znašal 5,1 %, v drugih državah EU pa kar 5,42 %. Očitno je, da je slovenski nevladni
      sektor v primerjavi z drugimi državami EU kadrovsko precej zelo podhranjen.
      <br />
      <br />
      Pri doseganju družbenih sprememb in izvajanju storitev, ki jih država ne zagotavlja, so
      organizacije civilne družbe ključnega pomena.
    </p>
    <div class="button share">
      <span>DELI S PRIJATELJI</span>
      <a :href="`https://twitter.com/intent/tweet?text=${twitterText}`"
        class="btn btn-social js-twitter myhover"
        target="_blank"
      >
        <svg width="35" height="35" viewBox="0 0 1792 1792" xmlns="http://www.w3.org/2000/svg">
          <path
            d="M1684 408q-67 98-162 167 1 14 1 42 0 130-38 259.5t-115.5 248.5-184.5
              210.5-258 146-323 54.5q-271 0-496-145 35 4 78 4 225 0
              401-138-105-2-188-64.5t-114-159.5q33 5 61 5 43 0
              85-11-112-23-185.5-111.5t-73.5-205.5v-4q68 38 146 41-66-44-105-115t-39-154q0-88
              44-163 121 149 294.5 238.5t371.5 99.5q-8-38-8-74 0-134 94.5-228.5t228.5-94.5q140
              0 236 102 109-21 205-78-37 115-142 178 93-10 186-50z">
          </path>
        </svg>
      </a>
      <a :href="facebookLink"
        class="btn btn-social js-facebook myhover">
        <svg width="35" height="35" viewBox="0 0 1792 1792" xmlns="http://www.w3.org/2000/svg">
          <path
            d="M1343 12v264h-157q-86 0-116 36t-30 108v189h293l-39
            296h-254v759h-306v-759h-255v-296h255v-218q0-186 104-288.5t277-102.5q147
            0 228 12z">
          </path>
        </svg>
      </a>
    </div>
    <a target="_blank" href="https://edavki.durs.si/EdavkiPortal/OpenPortal/CommonPages/Opdynp/PageD.aspx?category=namenitev_dela_dohodnine_fo" class="button support">NAMENI DOHODNINO</a>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

@Component
export default class Support extends Vue {
  get twitterText() {
    console.log(this.$router.currentRoute);
    return encodeURIComponent(
      'Ali veš, kaj vse počnejo organizacije civilne družbe?\nPreveri svoje znanje in se nauči še kaj novega v naši interaktivni spletni igri! https://www.druzbenespremembe.org/igra/',
    );
  }

  get facebookLink() {
    console.log(this.$router.currentRoute);
    const appId = '123123123';
    const url = 'https://www.druzbenespremembe.org/igra/';
    return `https://www.facebook.com/dialog/feed?app_id=${appId}&redirect_uri=${url}&link=${url}&ref=responsive`;
  }
}
</script>

<style lang="scss">
.share {
  a {
    display: none;
  }

  &:hover {
    span {
      display: none;
    }
    a {
      display: inline-block;
    }
  }
}
</style>
