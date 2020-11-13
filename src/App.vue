<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<style lang="scss">
 @import url('https://fonts.googleapis.com/css2?family=Raleway:ital,wght@0,400;0,600;0,800;1,900&display=swap');

body {
  background-color: #000000;
  padding: 0;
  margin: 0;
}
#app {
  font-family: Raleway;
  text-align: center;
  color: #ffffff;

  padding-top: 20px;

  h1 {
    font-weight: 900;
    font-style: italic;
    text-transform: uppercase;
    font-size: 40px;
    margin-top: 30px;
    margin-bottom: 30px;
  }

  p {
    color: #ffffff;
    font-size: 20px;
    font-weight: 400;
    line-height: 34px;

    max-width: 800px;
    margin: auto;
    margin-bottom: 80px;
  }

  button,
  a.button,
  div.button {
    min-width: 358px;
    height: 75px;
    border-radius: 38px;
    background-color: #f5f1e4;

    color: #000000;
    font-size: 36px;
    font-weight: 900;
    line-height: 75px;
    text-align: center;

    cursor: pointer;

    text-decoration: none;
    display: inline-block;

    padding-left: 30px;
    padding-right: 40px;
    margin-left: 10px;
    margin-right: 10px;
    margin-bottom: 20px;

    &::after {
      content: '';
      display: inline-block;

      width: 0;
      height: 0;
      border-style: solid;
      border-width: 16px 0 16px 27px;
      border-color: transparent transparent transparent #000000;

      position: relative;
      top: 3px;
      left: 20px;

      transition: transform 0.4s ease-out;
    }

    &:hover {
      &::after {
        transform: rotate(360deg);
      }
    }

    &.support {
      background-color: #f5af22;

      &::after {
        border: none;
        width: 35px;
        height: 35px;
        background-image: url('./assets/heart-full.png');
        background-size: contain;
        background-repeat: no-repeat;

        top: 7px;
      }
    }

    &.share {
      &::after {
        border: none;
        width: 35px;
        height: 35px;
        background-image: url('./assets/share.png');
        background-size: contain;
        background-repeat: no-repeat;

        top: 4px;
      }
    }
  }
}

.logo-header {
  width: 100%;
  height: 80px;
  img {
    max-height: 100%;
    width: auto;
    margin-left: 10px;
    margin-right: 10px;

    &:nth-child(2) {
      margin-bottom: 34px;
    }
  }
}
</style>
