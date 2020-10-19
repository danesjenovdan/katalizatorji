<template>
  <div
    class="game"
    @keyup.right="moveRight"
    @keyup.left="moveLeft"
  >
    <!-- <div class="controls">
      <textarea v-model="circleJSON"></textarea>
      <button @click="restartGame">Update</button>
    </div> -->
    <div class="nav">
      <div class="hearts">
        <div
          v-for="heart in 3"
          :key="heart"
          :class="['heart', { empty: lives < heart }]"
          ></div>
      </div>
      <img src="../assets/logo.png">
      <div class="points">{{ points }}</div>
    </div>
    <div
      v-for="circle in circles"
      :key="circle.id"
      class="circle"
      :style="{
        top: `${circle.top + circleTop}px`,
        left: `${circle.left + leftPadding}px`,
        'background-image': `url('/problems/${circle.fileName}.png')`,
      }"
    ></div>
    <div class="buckets" :style="{ left: `${bucketsLeft}px` }">
      <div :class="['bucket', { shake: shakeBuckets }]">
        <div class="bucket-top">
          Država
        </div>
        <div class="bucket-bottom">
          <div class="bucket-icon"><img src="../assets/state.png"></div>
          <div class="bucket-progress-bar">
            <div
              class="bucket-progress-bar-progress"
              :style="{ width: `${stateWidth}%` }"
            ></div>
          </div>
        </div>
      </div>

      <div :class="['bucket', { shake: shakeBuckets }]">
        <div class="bucket-top">
          Organizacije<br />civilne družbe
        </div>
        <div class="bucket-bottom">
          <div class="bucket-icon"><img src="../assets/civil-society.png"></div>
          <div class="bucket-progress-bar">
            <div
              class="bucket-progress-bar-progress"
              :style="{ width: `${civilSocietyWidth}%` }"
            ></div>
          </div>
        </div>
      </div>

      <div :class="['bucket', { shake: shakeBuckets }]">
        <div class="bucket-top">
          Podjetja
        </div>
        <div class="bucket-bottom">
          <div class="bucket-icon"><img src="../assets/business.png"></div>
          <div class="bucket-progress-bar">
            <div
              class="bucket-progress-bar-progress"
              :style="{ width: `${businessWidth}%` }"
            ></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import CIRCLES from '../assets/circles';

@Component
export default class Game extends Vue {
  private bucketsLeft: number;

  private circles: object[];

  private circleTop: number;

  private overlaps: string[];

  private lives: number;

  private statePoints: number;

  private civilSocietyPoints: number;

  private businessPoints: number;

  private gameLoop: any;

  private circleJSON: string;

  private shakeBuckets: boolean;

  private pauseGame: boolean;

  private leftPadding: number;

  constructor() {
    super();
    this.bucketsLeft = (window.innerWidth - 1000) / 2;
    this.circles = this.generateGame();
    this.circleTop = 0;
    this.overlaps = [];
    this.lives = 3;
    this.statePoints = 0;
    this.civilSocietyPoints = 0;
    this.businessPoints = 0;
    this.circleJSON = JSON.stringify(CIRCLES);
    this.shakeBuckets = false;
    this.pauseGame = false;
    this.leftPadding = (window.innerWidth - 1000) / 2;

    // listen to key events
    window.addEventListener('keydown', (event) => {
      if (event.keyCode === 37) {
        this.moveLeft();
      } else if (event.keyCode === 39) {
        this.moveRight();
      }
    });

    // main game loop
    this.gameLoop = window.setInterval(() => {
      this.moveCircles();
    }, 500);

    // // enable touch controls
    // document.addEventListener('DOMContentLoaded', () => {
    //   this.$el.addEventListener('click', this.chooseSide);
    // });
  }

  get points() {
    return this.statePoints + this.civilSocietyPoints + this.businessPoints;
  }

  get stateWidth() {
    return (this.statePoints / 10) * 100;
  }

  get civilSocietyWidth() {
    return (this.civilSocietyPoints / 10) * 100;
  }

  get businessWidth() {
    return (this.businessPoints / 10) * 100;
  }

  getRandomCircle(circle: object) {
    let categoryLetter;
    let categoryMax;
    switch (circle.category) {
      case 0:
        categoryLetter = 'D';
        categoryMax = 8;
        break;
      case 1:
        categoryLetter = 'OCD';
        categoryMax = 34;
        break;
      case 2:
        categoryLetter = 'T';
        categoryMax = 6;
        break;
      default:
        alert('Ups, nekaj je šlo narobe.');
    }

    const newCircle = { ...circle };
    console.log(this.leftPadding);
    return {
      ...newCircle,
      fileName: `${categoryLetter}${Math.floor(Math.random() * categoryMax) + 1}`,
      shake: false,
    };
  }

  generateGame() {
    console.log(this.businessPoints);
    return CIRCLES.map((circle) => ({ ...this.getRandomCircle(circle) }));
  }

  restartGame() {
    window.clearInterval(this.gameLoop);

    this.bucketsLeft = 0;
    this.circles = JSON.parse(this.circleJSON);
    this.circleTop = 0;
    this.overlaps = [];
    this.lives = 3;
    this.statePoints = 0;
    this.civilSocietyPoints = 0;
    this.businessPoints = 0;

    // main game loop
    this.gameLoop = window.setInterval(() => {
      this.moveCircles();
    }, 500);
  }

  moveRight() {
    if (this.bucketsLeft < (window.innerWidth - 420)) {
      this.bucketsLeft += 50;
    }
  }

  moveLeft() {
    if (this.bucketsLeft > -840) {
      this.bucketsLeft -= 50;
    }
  }

  gameOver() {
    this.overlaps = [];
    this.circles = CIRCLES;
    clearInterval(this.gameLoop);
    this.$router.push('/game-over');
  }

  moveCircles() {
    if (!this.pauseGame) {
      this.circleTop += 40;
      const circles = this.$el.getElementsByClassName('circle');
      const buckets = this.$el.getElementsByClassName('bucket');
      buckets.forEach((bucket, bucketIndex) => {
        circles.forEach((circle, circleIndex) => {
          const rect1 = bucket.getBoundingClientRect();
          const rect2 = circle.getBoundingClientRect();

          const overlap = !(rect1.right < rect2.left - 20
            || rect1.left > rect2.right - 20
            || rect1.bottom < rect2.top - 20
            || rect1.top > rect2.bottom - 20);

          if (overlap) {
            this.overlaps.push(`${bucketIndex}${circleIndex}`);
            this.resolveOverlaps();
          }
        });
      });
    }
  }

  resolveOverlaps() {
    this.overlaps.forEach((overlap, overlapIndex) => {
      const bucketIndex = parseInt(overlap.substring(0, 1), 10);
      const circleIndex = parseInt(overlap.substring(1, 2), 10);
      const newCircle = { ...this.circles[circleIndex] };
      newCircle.top -= 4320;
      this.getRandomCircle(newCircle);
      this.circles.splice(circleIndex, 1, newCircle);

      if (newCircle.category === bucketIndex) {
        // award points
        switch (bucketIndex) {
          case 0:
            this.statePoints += 1;
            break;
          case 1:
            this.civilSocietyPoints += 1;
            break;
          case 2:
            this.businessPoints += 1;
            break;
          default:
            console.error('something happened');
        }

        // at 10 bucket points the game is over
        if (
          (this.statePoints === 10)
          || (this.civilSocietyPoints === 10)
          || (this.businessPoints === 10)
        ) {
          this.gameOver();
        }
      } else {
        // shake the buckets
        this.shakeBuckets = true;
        this.pauseGame = true;
        window.setTimeout(() => {
          this.shakeBuckets = false;
          this.pauseGame = false;
        }, 2000);

        // lose life
        this.lives -= 1;

        // at -1 lives the game is over
        if (this.lives === -1) {
          this.gameOver();
        }
      }
    });
    this.overlaps = [];
  }
}
</script>

<style lang="scss">
.game {
  background-color: #f5f1e4;
  min-height: 100vh;
  position: relative;
  overflow: hidden;

  .controls {
    position: fixed;
    width: 100%;
    height: 50px;
    z-index: 2;
    top: 100px;
  }

  .nav {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 110px;
    z-index: 1;

    background: #000000;

    .hearts {
      display: block;
      position: relative;
      float: left;
      padding-top: 30px;
      padding-left: 20px;

      .heart {
        width: 53px;
        height: 49px;
        background-image: url('../assets/heart-full.png');
        background-size: contain;
        background-repeat: no-repeat;
        display: inline-block;
        margin-right: 5px;

        &.empty {
          background-image: url('../assets/heart-empty.png');
        }
      }
    }

    img {
      display: block;
      width: 121px;
      height: 78px;
      margin-top: 15px;

      position: absolute;
      left: 50%;
      margin-left: -60px;
    }

    .points {
      display: block;
      position: relative;
      float: right;
      padding-top: 25px;
      padding-right: 20px;
      font-size: 46px;
      // line-height: 90px;

      &::before {
        content: '';
        display: inline-block;
        width: 45px;
        height: 43px;
        background-image: url('../assets/star.png');
        background-size: contain;
        background-repeat: no-repeat;
        position: relative;
        top: 6px;
        margin-right: 5px;
      }
    }
  }

  .circle {
    width: 150px;
    height: 150px;
    background-color: #cd2826;
    position: absolute;
    top: 0;
    left: 200px;
    background-size: contain;
    background-repeat: no-repeat;

    color: #ffffff;
    font-size: 16px;
    line-height: 150px;

    border-radius: 50%;
    transition: top 0.5s linear;

    animation-name: spin;
    animation-duration: 4s;
    animation-iteration-count: infinite;

    &.shake {
      animation: shake 1.5s;
    }
  }

  .buckets {
    position: absolute;
    bottom: 60px;
    width: 1120px;
    height: 150px;

    overflow: hidden;

    transition: left 0.2s ease-in;

    .bucket {
      width: 300px;
      height: 150px;
      position: relative;
      float: left;
      margin-left: 30px;
      margin-right: 30px;
      overflow: hidden;

      .bucket-top {
        width: 300px;
        height: 80px;
        background: #c4c1b6;

        clip-path: polygon(0 0, 100% 0, 85% 100%, 15% 100%);

        line-height: 80px;
        text-transform: uppercase;
        color: #000000;
        font-weight: 700;

        overflow: hidden;
      }

      &:nth-child(2) {
        .bucket-top {
          line-height: 20px;
          padding-top: 20px;
        }
      }

      .bucket-bottom {
        background: #ffffff;
        width: 300px;
        height: 70px;
        position: relative;
        border-radius: 35px;

        .bucket-icon {
          width: 42px;
          height: 42px;
          display: inline-block;
          overflow: hidden;
          top: 14px;
          position: relative;

          img {
            width: auto;
            height: auto;
            max-width: 42px;
            max-height: 42px;
          }

          margin-right: 5px;
        }

        .bucket-progress-bar {
          width: 220px;
          height: 30px;
          background: #000000;
          display: inline-block;
          border-radius: 15px;
          position: relative;
          top: 8px;

          .bucket-progress-bar-progress {
            width: 0;
            height: 30px;
            border-radius: 15px;
            background-color: #cd2826;
          }
        }
      }

      &:nth-child(2) {
        .bucket-bottom {
          margin-top: -20px;
        }
      }

      &.shake {
        animation: shake 1.5s;
      }
    }
  }
}

@keyframes spin {
  from {
    transform:rotate(0deg);
  }
  to {
    transform:rotate(360deg);
  }
}

@keyframes shake {
  0% { transform: translate(1px, 1px) rotate(0deg); }
  10% { transform: translate(-1px, -2px) rotate(-1deg); }
  20% { transform: translate(-3px, 0px) rotate(1deg); }
  30% { transform: translate(3px, 2px) rotate(0deg); }
  40% { transform: translate(1px, -1px) rotate(1deg); }
  50% { transform: translate(-1px, 2px) rotate(-1deg); }
  60% { transform: translate(-3px, 1px) rotate(0deg); }
  70% { transform: translate(3px, 1px) rotate(-1deg); }
  80% { transform: translate(-1px, -1px) rotate(1deg); }
  90% { transform: translate(1px, 2px) rotate(0deg); }
  100% { transform: translate(1px, -2px) rotate(-1deg); }
}
</style>
